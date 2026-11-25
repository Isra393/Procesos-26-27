# Sprint 1 — Resumen

Estado de las fuentes: 25 de noviembre de 2026.

Resumen reconstruido a partir de `git log --date=short`, del
[README](../README.md) y de los archivos del repositorio. No reproduce memoria
literal de conversaciones ni añade una retrospectiva que no esté registrada.

## Hito 1 — Estructura, usuarios y CI

Fechas observables: 30 de septiembre y 9 de octubre de 2026.

- Commit inicial del proyecto y notas de presentación.
- Estructura por capas con cliente, servidor, pruebas y SQL.
- Gestión de usuarios en memoria y exposición mediante API.
- GitHub Actions ejecutando las pruebas automáticas.

Evidencia: `103a2e6`, `2b707ea`, `4c0e825`, `c9e6c6e` y
`.github/workflows/ci.yml`.

## Hito 2 — Registro, sesiones y rutas protegidas

Fechas observables: 9 y 10 de octubre de 2026.

- Registro local con hash de contraseña.
- Autenticación y sesiones en memoria.
- Interfaz de registro y sesión conectada con la API.
- Perfil protegido y eliminación de la propia cuenta.

Evidencia: `08f5701`, `bec2673`, `77d6405`, `08732a5` y
`test/autenticacion.test.js`.

## Hito 3 — Persistencia, roles, logs y Cloud Run

Fecha observable: 10 y 11 de octubre de 2026.

- Persistencia de usuarios con PostgreSQL y consultas parametrizadas.
- Arranque preparado para Cloud Run.
- Roles `usuario` y `administrador` con autorización en servidor.
- Logs JSON de actividad con campos cerrados y sin secretos.

Evidencia: `ea94a0c`, `0c8cbc6`, `3715e9a`, `113154b`,
`sql/001-usuarios.sql`, `sql/002-roles.sql` y `test/actividad.test.js`.

## Hito 4 — OAuth, confirmación y cierre

Fechas observables: 15, 21, 22 y 23 de octubre de 2026.

- Normalización y validación de correo.
- Google OAuth/OpenID Connect con identidad por `sub`.
- Confirmación de cuenta por correo y límite de envíos.
- Mejoras de cuentas: reutilización de correo tras la baja y contraseñas.
- Corrección del diagnóstico seguro de errores OAuth.
- Cierre del Sprint 1.

Evidencia: `5d8182d`, `8c615e3`, `e3bac9e`, `ff0b23c`, `763659d`,
`da7006e`, `test/oauth.test.js`, `test/confirmacion.test.js` y
`sql/003-oauth-google.sql`, `sql/004-confirmacion-correo.sql`,
`sql/005-correos-disponibles.sql`.

## Resultado documentado

Al cierre del Sprint 1 el README describe registro, confirmación por correo,
login, sesiones de 8 horas, logout, perfil, roles, baja lógica, Google OAuth,
PostgreSQL, logs JSON y despliegue en Cloud Run. La suite histórica del Sprint 2
se registra después con 229/229 pruebas generales; este resumen no atribuye al
Sprint 1 conteos que no consten.

## Límites

- No se conserva en este documento una narración diaria del Sprint 1.
- Las fechas son las de Git; no se convierten en fechas de reuniones o entregas
  no registradas.
- Las validaciones manuales de OAuth, correo real y Cloud pertenecen al
  responsable del proyecto y no se presentan como pruebas del agente.
