# Decisiones documentadas

Estado de las fuentes: 25 de noviembre de 2026.

Cada entrada separa el **hecho observable** del **motivo respaldado**. Cuando el
repositorio o el [README](../README.md) no explican el motivo, se marca como
inferencia y no se completa con una justificación inventada. No se asignan
fechas que no consten en Git o en la documentación.

Fuentes revisadas: README, `package.json`, `compose.yml`, `sql/`,
`.github/workflows/ci.yml`, `Servidor/` y `docs/sprint3/`. No se consultaron
paneles de Cloud, bases de producción ni credenciales reales.

| ID | Decisión | Hecho observable | Motivo respaldado |
|---|---|---|---|
| D01 | Node.js 24 con módulos ES | `package.json` declara `type: module` y `engines.node: >=24.19.0 <25`. | El README cita mismo lenguaje en cliente y servidor con capas separadas. |
| D02 | HTTP nativo, sin framework de servidor | `package.json` solo declara `google-auth-library`, `nodemailer` y `pg`; el servidor usa módulos de Node. | El README indica HTTP nativo y ausencia de frameworks añadidos. |
| D03 | Cliente HTML, CSS y JavaScript sin compilación | `Cliente/` contiene HTML, CSS y JS servidos por el backend. | El README afirma que no hay dependencias de cliente ni compilación. |
| D04 | PostgreSQL 17 con `pg` | `compose.yml` usa `postgres:17`; `pg` figura en dependencias; `sql/` define el esquema. | El README cita persistencia relacional, SQL parametrizado y transacciones. |
| D05 | Migraciones ordenadas sin 007 | `sql/` contiene 001–006 y 008; el CI y el README repiten esa lista. | El README advierte de que no existe 007 en esta rama. |
| D06 | Sesión en cookie `HttpOnly` | El README describe cookie `HttpOnly`, `SameSite=Lax` y `Secure` en producción. | Motivo de seguridad indicado en el README; no se verifican cabeceras en vivo. |
| D07 | OAuth de Google resuelto en servidor | `Servidor/google-oauth.js` y el README describen PKCE, `state` y `nonce`. | El README justifica verificar firma, emisor, audiencia, caducidad y `nonce`. |
| D08 | TMDB solo desde el backend | El README prohíbe enviar `TMDB_READ_ACCESS_TOKEN` al navegador; el cliente usa un contrato propio. | Motivo de seguridad y normalización citado en el README. |
| D09 | Correo con Gmail SMTP para la demostración | `nodemailer` está en dependencias; el README describe `SMTP_USER` y `SMTP_PASSWORD`. | El README lo presenta como configuración de bajo volumen para la demo. |
| D10 | Frontend y API en el mismo origen | El backend sirve estáticos y rutas `/api`; el README lo declara. | El README evita CORS y mantiene la cookie en el mismo origen. |
| D11 | Cloud Run, Cloud SQL y Secret Manager | El README documenta URL pública, Cloud SQL y secretos. | Motivo operativo descrito en el README; no hay configuración de red versionada. |
| D12 | CI con GitHub Actions | `.github/workflows/ci.yml` ejecuta `npm test` y `npm run test:postgres`. | El workflow prepara PostgreSQL 17 y aplica 001–006 y 008. |
| D13 | Despliegue separado de la CI | El README menciona Cloud Build para construcción y despliegue. | Inferencia: el repositorio no incluye `cloudbuild.yaml`; la separación se acepta solo como afirmación del README. |
| D14 | Recuperación con token de un solo uso | `sql/008` y los tests de recuperación cubren token, caducidad y consumo. | El README indica SHA-256, 30 minutos y revocación de sesiones. |
| D15 | Listas no integradas | El README y `docs/sprint3/semana-1.md` citan PR #24 cerrado y PR #27 abierto. | No hay migración 007 ni evidencia de integración; no se afirma lo contrario. |

## Notas de interpretación

- D11 y D13 describen intención operativa, no una auditoría de la cuenta cloud.
  No se deducen direcciones IP, certificados, reglas de firewall ni cadenas de
  conexión distintas de las publicadas en el README.
- D06 se apoya en la documentación; no se comprueba aquí una respuesta HTTP real
  con `Set-Cookie`.
- D05 y D15 son límites verificables en el árbol de trabajo. Cualquier cambio
  futuro debe actualizar el README, el CI y este documento a la vez.
- Las referencias visuales a Letterboxd y JustWatch no son decisiones de
  integración: el README las limita a inspiración de interfaz.
