# Sprint 3 — Documentación

Documentación del Sprint 3 de CineMatch. La recuperación de contraseña local ya
está integrada; las listas siguen pendientes y no se afirma su integración ni la
migración 007, que no existe en esta rama.

## Calendario

| Semana | Periodo | Cierre y revisión |
|---|---|---|
| Semana 1 | 19–25 de noviembre de 2026 | Cierre 25 nov a las 23:59 (Europe/Madrid); revisión 26 nov |
| Semana 2 | 26 de noviembre–2 de diciembre de 2026 | Seguimiento semanal |
| Semana 3 | 3–10 de diciembre de 2026 | Cierre del sprint y memoria final |

## Documentos

- [Semana 1 — Evidencias y seguimiento](semana-1.md): aportaciones externas,
  trabajo propio, feedback recibido, pruebas conocidas y pendientes.
- [Issue #25 — Recuperación de contraseña](issue-25-recuperacion-password.md):
  alcance, contrato HTTP, seguridad, migración 008, pruebas históricas y
  validación manual en Cloud aportada por el responsable del proyecto.

## Estado al 25 de noviembre de 2026

- La recuperación de contraseña local (#25) está integrada mediante el
  [PR #26](https://github.com/chemaa14/Procesos-26-27/pull/26), fusionado. El
  responsable del proyecto confirmó la migración 008 en Cloud SQL y el
  funcionamiento en Cloud; el agente no realizó pruebas propias de Gmail ni de
  Cloud.
- Las aportaciones externas de la semana 1 se registran por separado en
  [semana-1.md](semana-1.md), con su estado real en GitHub.
- Listas: el [PR #24](https://github.com/chemaa14/Procesos-26-27/pull/24) está
  cerrado sin integrar y el [PR #27](https://github.com/chemaa14/Procesos-26-27/pull/27)
  sigue abierto y pendiente. La revisión local del PR #27 deja 254 pruebas
  generales superadas y 24/25 con PostgreSQL; falla
  `integracion/api-listas-postgres.js:162` por `servidor2.sesiones` indefinido.

La memoria final se completará al terminar la semana 3.
