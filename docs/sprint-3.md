# Sprint 3 — Resumen

Estado de las fuentes: 25 de noviembre de 2026.

Documento de resumen. El detalle operativo, las evidencias y el seguimiento
semanal están en [docs/sprint3](sprint3/README.md). No se afirma que la semana 2
esté cerrada ni se inventan fechas posteriores al 25 de noviembre.

## Alcance

- Recuperación de contraseña local ya integrada.
- Seguimiento de listas pendiente.
- Recomendaciones, reseñas, valoraciones, historial y funciones sociales fuera
  de alcance.
- Documentación de la semana 1 con aportaciones externas, trabajo propio y
  feedback recibido.

## Recuperación de contraseña

La funcionalidad permite solicitar un enlace de un solo uso y restablecer la
contraseña sin iniciar sesión. El token se almacena como SHA-256, caduca a los
30 minutos, invalida el anterior al reenviar y revoca las sesiones al cambiar la
contraseña. Se aplican límites de 60 segundos, cinco por cuenta/hora y 100
globales/hora.

Evidencia: `sql/008-recuperacion-password.sql`, `test/api-recuperacion.test.js`,
`test/recuperacion.test.js`, `test/correo-recuperacion.test.js` e
`integracion/recuperacion-postgres.js`. La issue #25 está cerrada y el PR #26
fusionado según el [README](../README.md).

## Estado de listas

- PR #24 cerrado sin integrar.
- PR #27 abierto y pendiente.
- La revisión local del PR #27 registra 254 pruebas generales superadas y 24/25
  con PostgreSQL; falla `integracion/api-listas-postgres.js:162` por
  `servidor2.sesiones` indefinido.
- No existe migración 007 en esta rama. No se afirma la integración de listas ni
  la aplicación de esa migración.

## Evidencias de la semana 1

- [Semana 1 — evidencias y seguimiento](sprint3/semana-1.md): aportaciones
  externas, trabajo propio, feedback, pruebas conocidas y pendientes.
- [Issue #25 — recuperación de contraseña](sprint3/issue-25-recuperacion-password.md):
  contrato HTTP, seguridad, migración y límites de validación.
- [Índice del Sprint 3](sprint3/README.md): calendario y estado.

Las aportaciones externas registradas son dos issues y dos pull requests de la
semana 1. La validación de la migración 008 en Cloud SQL y del flujo en Cloud la
aporta el responsable del proyecto; el agente no realizó pruebas propias de
Gmail real ni de Cloud.

## Pendientes

- Seguir la PR #26 externa de despensa-inteligente sin adelantar su estado.
- Resolver o aclarar el fallo de PostgreSQL del PR #27 antes de afirmar una
  integración.
- Preparar la memoria final al cerrar la semana 3.
- Mantener separadas las aportaciones externas, el trabajo propio y el feedback.
