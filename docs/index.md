# CineMatch — Índice de documentación

Estado de las fuentes: 25 de noviembre de 2026.

Este índice reúne la documentación transversal de CineMatch y enlaza los
documentos de sprint ya existentes. La organización de carpetas se inspira en la
[documentación de Querencia](https://github.com/JoseJavierML/Querencia/tree/main/docs);
esa referencia es solo estructural. No se copian contenidos de Querencia ni se
incorporan sus decisiones de stack.

## Lectura recomendada

1. [README del repositorio](../README.md): producto, ejecución, API, pruebas y
   despliegue.
2. [Arquitectura](arquitectura.md): capas, datos e integraciones externas.
3. [Requisitos](requisitos.md): requisitos documentales propios y estado.
4. [Decisiones](decisiones.md): decisiones observables y su respaldo.
5. [Procesos](procesos.md): roles, revisión, integración continua y secretos.
6. [Cronología](log.md): hitos fechados con commits reales.
7. Documentos de sprint: [Sprint 1](sprint-1.md), [Sprint 2](sprint-2.md) y
   [Sprint 3](sprint-3.md).

## Documentos generales

| Documento | Contenido |
|---|---|
| [README](../README.md) | Presentación, estado, comandos, API y operación. |
| [Arquitectura](arquitectura.md) | Cliente, servidor, datos, TMDB, correo, OAuth y nube. |
| [Decisiones](decisiones.md) | Decisiones D01–D15 con hecho observable y límites. |
| [Procesos](procesos.md) | Roles de opencode, ChatGPT y responsable del proyecto. |
| [Requisitos](requisitos.md) | Tabla de requisitos con evidencia y pendientes. |
| [Cronología](log.md) | Historial fechado a partir de `git log`. |
| [Sprint 1](sprint-1.md) | Resumen de los hitos 1 a 4. |
| [Sprint 2](sprint-2.md) | Resumen de S2-01, S2-02 y mejora de interfaz. |
| [Sprint 3](sprint-3.md) | Recuperación de contraseña, listas y evidencias. |
| [AGENTS](../AGENTS.md) | Protocolo de colaboración y convenciones técnicas. |

## Documentación de sprint existente

- [Sprint 2 — documentos por tarea](sprint2/): fuente de datos, catálogo,
  persistencia, API, selector, disponibilidad y pruebas.
- [Sprint 3 — índice](sprint3/README.md): calendario, semana 1 e issue #25.
- [Sprint 3 — semana 1](sprint3/semana-1.md): aportaciones externas, trabajo
  propio, feedback y pruebas conocidas.
- [Sprint 3 — recuperación de contraseña](sprint3/issue-25-recuperacion-password.md):
  contrato, seguridad, migración 008 y límites de validación.

## Alcance y límites

- Estado documentado a 25 de noviembre de 2026. No se afirma que la semana 2 del
  Sprint 3 esté cerrada ni se inventan fechas posteriores.
- La recuperación de contraseña local está integrada. Las listas siguen
  pendientes: el PR #24 está cerrado sin integrar y el PR #27 abierto.
- No existe la migración 007 en esta rama. Las migraciones aplicables son 001 a
  006 y 008.
- Las referencias a Querencia, DoneTonic, Letterboxd o JustWatch son
  organizativas o visuales; no implican copia de código, datos ni stack.
- Los detalles operativos no verificables en el repositorio se marcan como
  límites en [Arquitectura](arquitectura.md) y [Decisiones](decisiones.md).
