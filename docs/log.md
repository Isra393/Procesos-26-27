# Cronología documental

Estado de las fuentes: 25 de noviembre de 2026. Las fechas de commits proceden de
`git log --date=short`. No se añaden fechas de memoria ni se afirma trabajo de la
semana 2 del Sprint 3.

## Hitos del repositorio

| Fecha | Hito | Evidencia |
|---|---|---|
| 2026-09-30 | Commit inicial y primeras notas del proyecto. | `425bcc7`, `0e97f4f`, `ed4e975`. |
| 2026-10-09 | Estructura por capas, CI, usuarios en memoria y API. | `103a2e6`, `c9e6c6e`, `2b707ea`, `4c0e825`. |
| 2026-10-10 | Sesiones, interfaz de sesión y rutas protegidas. | `bec2673`, `77d6405`, `08732a5`. |
| 2026-10-10 | Persistencia de usuarios con PostgreSQL. | `ea94a0c`. |
| 2026-10-11 | Arranque para Cloud Run, roles y logs. | `0c8cbc6`, `3715e9a`, `113154b`. |
| 2026-10-15 | Normalización y validación de correo. | `5d8182d`. |
| 2026-10-21 | Google OAuth, sesiones persistentes y diagnóstico. | `8c615e3`, `e3bac9e`. |
| 2026-10-22 | Confirmación por correo y mejoras de cuentas. | `ff0b23c`, `763659d`. |
| 2026-10-23 | Cierre del Sprint 1. | `da7006e`, merge `364d383`. |
| 2026-11-12 | S2-01: TMDB, búsqueda paginada, ficha y pruebas. | `39c465f`, `0b7bd59`, `6de51bd`. |
| 2026-11-12 | S2-02: plataformas, persistencia y API. | `3a9dbee`. |
| 2026-11-13 | S2-02: selector y disponibilidad. | `5632fe7`. |
| 2026-11-13 | Mejora de interfaz y README de Sprint 2. | `125c209`, merge `234640e`. |
| 2026-11-22 | Logos de proveedores en ficha y selector. | `12606d7`. |
| 2026-11-24 | Recuperación de contraseña local integrada. | `02ee4fe`; PR #26 y migración 008 en el README. |
| 2026-11-25 | Revisión documental de la semana 1 del Sprint 3. | `docs/sprint3/semana-1.md`; sin commit asociado en esta rama. |

## Aportaciones externas de la semana 1

El detalle, los enlaces y los conteos de pruebas están en
[docs/sprint3/semana-1.md](sprint3/semana-1.md). Fechas registradas allí:

- 23 de noviembre de 2026: issue #25 en Isra393/despensa-inteligente y PR #2 en
  MariaMartinez128/Brote.
- 24 de noviembre de 2026: issue #24 en B1lly05/SplitMate.
- 25 de noviembre de 2026: PR #26 en Isra393/despensa-inteligente.

La PR #2 de Brote se registra como integrada el 25 de noviembre según la evidencia
de la semana 1. La PR #26 de despensa-inteligente permanece abierta. No se
extrapolan estos estados a fechas posteriores.

## Trabajo propio y feedback

- La recuperación de contraseña local consta integrada mediante la issue #25
  cerrada y el PR #26 fusionado, con la migración 008.
- El PR #23 de logos se registra fusionado el 24 de noviembre.
- El PR #24 de listas está cerrado sin integrar. El PR #27 sigue abierto.
- La validación de la migración 008 en Cloud SQL y del flujo en Cloud la aporta
  el responsable del proyecto; no hay prueba automática de Gmail real ni de
  Cloud Run.
- No hay PR publicada en el proyecto de Ana. El intento local quedó aparcado y no
  se contabiliza como aportación publicada.

## Límites

- La semana 2 del Sprint 3 no se documenta como terminada.
- No existe migración 007 en esta rama.
- Las fechas de aportaciones externas son las de la evidencia de semana 1, no
  una reconstrucción posterior.
