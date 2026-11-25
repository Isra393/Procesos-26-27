# Arquitectura de CineMatch

Estado de las fuentes: 25 de noviembre de 2026.

## Vista general

CineMatch es una aplicación web monolítica con dos capas desplegadas en el mismo
origen: un cliente HTML/CSS/JavaScript y un servidor HTTP nativo de Node.js 24
con módulos ES. La lógica de negocio, el acceso a datos y las integraciones
externas permanecen en el servidor. PostgreSQL 17 es la persistencia.

Evidencias principales: `package.json`, `compose.yml`, `Cliente/`, `Servidor/`,
`sql/`, `.github/workflows/ci.yml` y el [README](../README.md).

## Capas

| Capa | Ubicación | Responsabilidad |
|---|---|---|
| Presentación | `Cliente/index.html`, `Cliente/estilos.css`, `Cliente/*.js` | Formularios, catálogo, ficha, plataformas y administración. |
| API HTTP | `Servidor/api.js`, `Servidor/inicio-postgres.js` | Rutas, validación, archivos estáticos, cookies y autorización. |
| Lógica | `Servidor/logica.js`, `busqueda-peliculas.js`, `detalle-pelicula.js`, `disponibilidad-pelicula.js` | Reglas de negocio y normalización de datos. |
| Datos | `Servidor/datos-postgres.js`, `*postgres.js`, `pg` | SQL parametrizado, transacciones y persistencia. |
| Integraciones | `Servidor/catalogo-tmdb.js`, `google-oauth.js`, `correo.js` | TMDB, Google OAuth/OpenID Connect y Gmail SMTP. |
| Operación | `Servidor/actividad.js`, `sql/`, Cloud Run | Logs JSON, migraciones y configuración de ejecución. |

El cliente usa `textContent` para textos de usuario y no recibe secretos. La API
y el frontend comparten origen, de modo que la cookie de sesión no depende de
CORS.

## Datos y migraciones

Las migraciones reales de esta rama son `sql/001-usuarios.sql` a
`sql/006-preferencias-plataformas.sql` y `sql/008-recuperacion-password.sql`.
No existe `007` en esta rama.

| Migración | Objeto observable |
|---|---|
| 001 | Tabla `usuarios`. |
| 002 | Columna `rol` en `usuarios`. |
| 003 | `google_sub`, tablas `sesiones` e `intentos_oauth`. |
| 004 | `confirmaciones_correo` y `limite_correo`. |
| 005 | Índices únicos de correo e identidad Google para cuentas vigentes. |
| 006 | Tabla `preferencias_plataformas` por cuenta y región `ES`. |
| 008 | Tabla `recuperaciones_password`, token y caducidad. |

El CI aplica exactamente esas migraciones antes de ejecutar las pruebas con
PostgreSQL. La convergencia del esquema en Cloud SQL no se deduce del
repositorio; el [README](../README.md) registra que la 008 se aplicó allí y que
el responsable del proyecto confirmó el funcionamiento.

## Integraciones externas

- **TMDB:** solo el backend usa `TMDB_READ_ACCESS_TOKEN`. El cliente consume un
  contrato propio normalizado y nunca recibe el token. La disponibilidad se
  limita a `results.ES` de `watch/providers`.
- **Gmail SMTP:** Nodemailer envía confirmaciones y recuperación de contraseña.
  `SMTP_USER` y `SMTP_PASSWORD` viven en el servidor o en Secret Manager; no son
  el secreto OAuth.
- **Google OAuth/OpenID Connect:** el flujo se resuelve en el servidor con PKCE,
  `state` y `nonce`. Los tokens de Google no se entregan al frontend ni se
  registran en logs.

## Despliegue

La aplicación pública se sirve en Cloud Run. La persistencia prevista es Cloud
SQL y los secretos se referencian desde Secret Manager, según el
[README](../README.md). El mismo backend sirve el frontend y la API, por lo que
se mantiene un único origen público.

El README separa la CI de GitHub Actions del despliegue con Cloud Build. En esta
rama no hay `cloudbuild.yaml` ni Dockerfile versionado, así que la configuración
exacta de construcción, IP, SSL o conectores de Cloud SQL no es verificable y no
se inventa aquí. Tampoco se afirman nombres de secretos, cuentas de servicio o
directivas de red distintos de los citados en el README.

## Límites

- No hay pruebas automatizadas de Gmail real ni de Cloud Run en esta rama.
- La validación en Cloud SQL y Cloud Run la aporta el responsable del proyecto.
- El repositorio no demuestra por sí solo la topología de red, TLS ni los
  permisos efectivos de la cuenta de servicio.
- Las listas no forman parte de la arquitectura integrada: no hay migración 007
  ni PR fusionado de listas.
