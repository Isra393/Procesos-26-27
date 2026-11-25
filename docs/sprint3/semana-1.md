# Sprint 3 — Semana 1 (19–25 de noviembre de 2026)

- **Sprint:** 3
- **Periodo:** 19–25 de noviembre de 2026, cierre a las 23:59 (Europe/Madrid).
- **Revisión:** 26 de noviembre de 2026.
- **Alcance:** documentación de evidencias de la semana 1. Esta tarea de
  documentación no modifica código de producto ni añade dependencias, variables
  de entorno o migraciones.
- **Objetivo personal:** dos issues y dos pull requests. Es una meta de trabajo,
  no una cuota obligatoria del profesorado.

## Objetivos de la semana

1. Registrar las aportaciones externas realizadas en otros proyectos y su
   estado real en GitHub a 25 de noviembre de 2026.
2. Separar esas aportaciones del trabajo propio en CineMatch y del feedback
   recibido, sin atribuir al agente pruebas manuales de Cloud o Gmail.
3. Documentar el estado de la recuperación de contraseña local y de las listas,
   manteniendo las evidencias históricas y sin afirmar integraciones que no
   constan.
4. Dejar preparado el seguimiento de la semana 2 y la memoria final del Sprint 3.

## Aportaciones externas

Evidencias verificadas en GitHub a 25 de noviembre de 2026:

| Fecha | Proyecto | Tipo | Enlace | Estado | Resultado |
|---|---|---|---|---|---|
| 23 nov 2026 | Isra393/despensa-inteligente | Issue #25 | <https://github.com/Isra393/despensa-inteligente/issues/25> | Abierta | Ranking singular/plural Tomate/Tomates. |
| 24 nov 2026 | B1lly05/SplitMate | Issue #24 | <https://github.com/B1lly05/SplitMate/issues/24> | Abierta | Exportación de gastos a CSV. |
| 23 nov 2026 | MariaMartinez128/Brote | PR #2 | <https://github.com/MariaMartinez128/Brote/pull/2> | Integrada el 25 nov | Fechas imposibles sin error 500. Conteo de pruebas no registrado. |
| 25 nov 2026 | Isra393/despensa-inteligente | PR #26 | <https://github.com/Isra393/despensa-inteligente/pull/26> | Abierta, no integrada | Unificar singular/plural del ranking. OpenCode implementó y ChatGPT revisó y repitió las pruebas: 178 pasan y 0 fallan; la suite de Mongo se omitió al no existir `MONGODB_URI_TEST`. La regresión falló antes del arreglo y pasó después. Archivos: `servidor/estadisticas.js` y `test/estadisticas.test.js`; sin variables de entorno ni migración. |

Resultado del objetivo personal: dos issues abiertas y dos pull requests
creadas (una integrada y otra aún abierta). La PR #26 no se cuenta como
integrada.

## Trabajo propio y feedback recibido

| Fecha | Proyecto | Tipo | Enlace | Estado | Resultado |
|---|---|---|---|---|---|
| 24 nov 2026 | chemaa14/Procesos-26-27 | Issue #25 (PATRIK) | <https://github.com/chemaa14/Procesos-26-27/issues/25> | Cerrada | Recuperación de contraseña local, integrada mediante el PR #26. |
| 24 nov 2026 | chemaa14/Procesos-26-27 | PR #26 | <https://github.com/chemaa14/Procesos-26-27/pull/26> | Fusionada | Recuperación integrada. Evidencias históricas: 246/246 pruebas generales y 18/18 con PostgreSQL. El responsable del proyecto confirmó la migración 008 en Cloud SQL y el funcionamiento en Cloud; la validación manual en Cloud corresponde al responsable del proyecto. El agente no aporta pruebas propias de Gmail real ni de Cloud. |
| 24 nov 2026 | chemaa14/Procesos-26-27 | PR #23 (JoseJavier) | <https://github.com/chemaa14/Procesos-26-27/pull/23> | Fusionada el 24 nov | Logos de proveedores en la ficha y el selector. |
| 24 nov 2026 | chemaa14/Procesos-26-27 | PR #24 (LuisLorenzo) | <https://github.com/chemaa14/Procesos-26-27/pull/24> | Cerrada sin integrar | Listas. Incluye [comentario propio](https://github.com/chemaa14/Procesos-26-27/pull/24#issuecomment-7125297408), con fecha del comentario 24 nov 2026. No se afirma la integración de listas. |
| 25 nov 2026 (revisión documental) | chemaa14/Procesos-26-27 | PR #27 (feedback) | <https://github.com/chemaa14/Procesos-26-27/pull/27> | Abierta a 25 nov 2026 | En la revisión local pasan 254 pruebas generales y 24 de 25 con PostgreSQL. Falla `integracion/api-listas-postgres.js:162` por `servidor2.sesiones` indefinido. No se afirma la integración de listas ni que la migración 007 esté aplicada: no existe 007 en esta rama. |

No hay una pull request publicada en el proyecto de Ana. El intento local quedó
aparcado por un bloqueo según el responsable del proyecto y no se cuenta como
aportación publicada.

## Alcance y pruebas conocidas

- Esta tarea de documentación no modifica código; ahora incluye documentación
  general en `docs/` además de README, AGENTS y documentos de Sprint 3.
- Organización documental completada: [docs/index.md](../index.md) enlaza
  arquitectura, decisiones, procesos, requisitos, `log.md` y los resúmenes de
  sprint. La carpeta de Querencia se usó solo como referencia estructural.
- Recuperación de contraseña: se conservan las evidencias históricas de
  246/246 pruebas generales y 18/18 con PostgreSQL. La validación en Cloud y la
  migración 008 en Cloud SQL las confirma el responsable del proyecto, no el
  agente. No se registran pruebas de entrega real de Gmail ni de Cloud Run.
- Listas: el PR #24 está cerrado sin integrar y el PR #27 sigue abierto. La
  revisión local del PR #27 registra 254 pruebas generales superadas y 24/25 con
  PostgreSQL, con el fallo indicado en `integracion/api-listas-postgres.js:162`.
  No se afirma integración ni migración 007.
- Aportación externa de Brote: se registra la integración de la PR #2 y el
  resultado funcional de fechas imposibles sin error 500. Conteo de pruebas no
  registrado.
- Aportación externa de despensa-inteligente: la PR #26 está abierta y no
  integrada. Se registran 178 pruebas superadas y 0 fallos, la omisión de la
  suite de Mongo sin `MONGODB_URI_TEST` y la regresión que falló antes del
  arreglo y pasó después.
- Comprobación local de esta revisión documental: `npm.cmd test` termina con
  **246/246 pruebas superadas y 0 fallos**. No se ejecuta
  `npm.cmd run test:postgres` porque esta revisión no toca código y no dispone
  de una base preparada; su registro histórico es 18/18.

## Pendientes para la semana 2 (26 nov–2 dic de 2026)

- Seguir la PR #26 externa de despensa-inteligente hasta su revisión o
  integración, sin adelantar su estado.
- Resolver o aclarar el fallo de PostgreSQL del PR #27 de listas antes de
  afirmar cualquier integración. No dar por aplicada la migración 007.
- Mantener la separación entre aportaciones externas, trabajo propio y feedback
  recibido en las evidencias de la semana 2.
- Preparar la memoria final del Sprint 3.

## Memoria final al terminar el Sprint 3

La memoria final se completará al cerrar la semana 3 (3–10 de diciembre de
2026). Debe recoger, como mínimo:

- objetivos y alcance real del sprint;
- aportaciones externas y trabajo propio, con enlaces y estados definitivos;
- feedback recibido y cambios aplicados;
- pruebas ejecutadas, con conteos exactos y limitaciones;
- decisiones, incidencias y pendientes;
- retrospectiva breve y evidencias de despliegue aportadas por el responsable
  del proyecto.
