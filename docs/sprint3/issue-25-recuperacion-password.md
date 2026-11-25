# Issue #25 — Recuperación de contraseña local

- **Sprint:** 3
- **Tarea:** #25 — Recuperación de contraseña
- **Fecha:** 24 de noviembre de 2026
- **Issue:** [#25](https://github.com/chemaa14/Procesos-26-27/issues/25), cerrada.
- **PR:** [#26](https://github.com/chemaa14/Procesos-26-27/pull/26), fusionado.
- **Estado:** implementada, probada en local y con PostgreSQL aislado, e
  integrada. El responsable del proyecto confirmó la migración 008 en Cloud SQL
  y el funcionamiento del flujo en Cloud; esa validación manual corresponde al
  responsable del proyecto y el agente no realizó pruebas propias de Gmail ni de
  Cloud.

## Alcance

Permite a una cuenta local confirmada y no eliminada recuperar su contraseña
mediante un enlace de un solo uso enviado por correo. No crea sesión automática,
no modifica cuentas Google-only y no revela si un correo existe. Las cuentas
pendientes, eliminadas o sin contraseña local no reciben enlace.

## Contrato HTTP

Ambas rutas son `POST`, exigen `Content-Type: application/json` y la cabecera
`X-CineMatch: 1`, no admiten parámetros de consulta ni campos extra y devuelven
JSON con `Cache-Control: no-store`.

| Método y ruta | Entrada | Respuesta |
|---|---|---|
| `POST /api/password/solicitar` | `{email}` | `202` con mensaje genérico |
| `POST /api/password/restablecer` | `{token,password}` | `200` con mensaje de éxito |

La solicitud devuelve siempre el mismo `202` y el mismo mensaje para una cuenta
local válida, un correo inexistente, una cuenta pendiente o eliminada, una
cuenta Google-only, un envío limitado o un fallo SMTP. El correo malformado
responde `400`. Solo si el servicio de recuperación no está inyectado en la
aplicación responde `503`; un fallo SMTP no cambia el `202`.

El restablecimiento devuelve `400 RECUPERACION_INVALIDA` para un token falso,
caducado o ya utilizado, y `400 PASSWORD_INVALIDA` si la contraseña no tiene
entre 8 y 128 caracteres Unicode. Una contraseña inválida no consume el token.
El éxito no inicia sesión: el usuario debe entrar con la nueva contraseña.

## Seguridad y persistencia

- Token de 256 bits con `crypto.randomBytes(32).toString("hex")`; solo se
  persiste su SHA-256. El token viaja en el fragmento
  `/#recuperar=TOKEN`, que el cliente elimina de la barra con
  `history.replaceState` antes de continuar.
- Caducidad de 30 minutos, un único token vigente por cuenta y uso único. Un
  reenvío invalida el anterior. El consumo concurrente solo puede triunfar una
  vez: PostgreSQL bloquea primero la cuenta y revalida el token bajo el bloqueo;
  en memoria no hay `await` entre las mutaciones.
- Al consumir se cambia el hash con scrypt, se revocan todas las sesiones de la
  cuenta y se anulan token y caducidad en la misma transacción. Un fallo hace
  rollback sin cambiar contraseña, token ni sesiones.
- Límites: 60 segundos entre envíos, 5 envíos por cuenta y hora y 100 envíos
  globales por hora. PostgreSQL comparte el cupo global con las confirmaciones
  mediante `limite_correo`. Los contadores se conservan tras consumir el token.
- Logs con eventos cerrados (`recuperacion_solicitada`,
  `recuperacion_enviada`, `password_restablecida`, `error_correo`). No se
  registran tokens, contraseñas ni direcciones de correo.
- La interfaz usa `textContent`, no guarda el token en almacenamiento del
  navegador, valida longitud y coincidencia, evita dobles envíos y muestra
  estados de carga, error y éxito. Tras el éxito vuelve al formulario de login.

Referencia: [OWASP Forgot Password Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html).
Se aplican sus recomendaciones de token aleatorio, caducidad y mensaje genérico;
no se ha medido la uniformidad temporal de las respuestas.

## Errores

| Estado | Significado |
|---|---|
| 400 | JSON, campos, email o token inválidos; contraseña fuera de rango |
| 403 | Falta la cabecera de protección de escritura |
| 405 | Método no permitido; incluye `Allow` |
| 413 / 415 | Cuerpo demasiado grande / tipo de contenido incorrecto |
| 503 | Servicio de recuperación no inyectado en la aplicación |
| 500 | Error interno genérico, sin detalles de SQL ni credenciales |

Un fallo SMTP durante la solicitud no altera la respuesta: se mantiene el `202`
genérico y solo se registra un `error_correo` con código cerrado, sin correo,
token ni credenciales.

## Migración y despliegue

La migración `sql/008-recuperacion-password.sql` crea
`recuperaciones_password` (una fila por cuenta, token único nullable, caducidad,
ventana y contador) con FK a `usuarios(id) ON DELETE CASCADE` y un índice por
caducidad. Ya se aplicó y verificó en la base aislada de pruebas. El responsable
del proyecto confirmó que también se aplicó en Cloud SQL antes del despliegue de
esta versión y que el flujo funciona en Cloud.

La cuenta de aplicación necesita:

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON public.recuperaciones_password TO cinematch_app;
```

No hay variables de entorno nuevas ni dependencias nuevas. Se reutilizan
`DB_*`, `SMTP_USER`, `SMTP_PASSWORD` y `APP_URL`. El arranque de PostgreSQL
exige una configuración SMTP válida: si falta o es incorrecta, el servidor no
arranca. El `503` de estas rutas solo se produce si `crearAplicacion` recibe el
servicio de recuperación ausente. Con SMTP operativo pero un envío fallido, la
solicitud sigue devolviendo `202` genérico y registra un log seguro; nunca
confirma si el correo es válido. La comprobación manual en Cloud corresponde al
responsable del proyecto; este documento no registra pruebas de Gmail real
realizadas por el agente.

## Pruebas realizadas

- Quince pruebas nuevas aisladas (`test/recuperacion.test.js`,
  `test/api-recuperacion.test.js`, `test/correo-recuperacion.test.js`):
  token, caducidad, reenvío, límites por cuenta y globales, fallo SMTP,
  cuentas no elegibles, consumo concurrente, contrato HTTP, campos extra,
  query, contraseña inválida sin consumo y correo sin secretos.
- `npm.cmd test`: **246/246 superadas, 0 fallos** (36,4 s).
- `npm.cmd run test:postgres` sobre PostgreSQL 17 aislado y desechable:
  **18/18 superadas, 0 fallos** (5,6 s). Las cinco nuevas cubren persistencia
  entre pools, caducidad, consumo único, concurrencia, rollback, aislamiento,
  cuentas no elegibles y límites.
- `node --check` correcto en todos los archivos nuevos y modificados.
- Validación visual realizada por ChatGPT en navegador local con una cuenta
  ficticia y correo simulado: la solicitud muestra el mensaje genérico, el
  fragmento se retira automáticamente al abrir el enlace, el panel de nueva
  contraseña valida campos vacíos, cancelar vuelve al login y a 375 px no hay
  overflow. No se probó Gmail real ni se restablecieron credenciales reales en
  el navegador.
- En el momento de la implementación, el agente no envió correos reales ni
  probó Cloud SQL, Cloud Run o el flujo manual completo con Gmail. Con
  posterioridad, el responsable del proyecto confirmó la migración 008 en Cloud
  SQL y el funcionamiento en Cloud; esa validación manual corresponde al
  responsable del proyecto y el agente no dispone de pruebas propias de Gmail ni
  de Cloud.

## Repetir la prueba manual en local

1. Antes de arrancar, aplicar la migración 008 a la base de desarrollo
   existente, sin borrar el volumen:

   ```powershell
   Get-Content -Raw -Encoding UTF8 .\sql\008-recuperacion-password.sql | docker compose exec -T db psql -U cinematch -d cinematch -v ON_ERROR_STOP=1
   ```

2. Reutilizar el `.env` existente (no hay variables nuevas; el arranque exige
   `SMTP_USER`, `SMTP_PASSWORD` y `APP_URL` válidos) y arrancar con
   `npm.cmd run start:postgres`.
3. Registrarse, confirmar la cuenta y cerrar sesión.
4. Pulsar «¿Has olvidado tu contraseña?», introducir el correo y comprobar el
   mensaje genérico.
5. Abrir el enlace recibido: el fragmento debe desaparecer de la barra y
   mostrarse el formulario de nueva contraseña.
6. Probar una contraseña corta (error sin consumir el token), después una
   válida y comprobar que vuelve al login sin sesión iniciada.
7. Verificar que la contraseña anterior ya no entra, que la nueva sí y que las
   sesiones abiertas antes del cambio quedaron revocadas.
8. Reutilizar el enlace: debe responder `RECUPERACION_INVALIDA`.

No pegar tokens, contraseñas ni cookies en la consola. El enlace de correo
caduca a los 30 minutos y solo sirve una vez.
