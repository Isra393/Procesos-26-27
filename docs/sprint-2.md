# Sprint 2 — Resumen

Estado de las fuentes: 25 de noviembre de 2026.

Resumen basado en el [README](../README.md), los documentos de
[docs/sprint2](sprint2/) y los commits de Git. La memoria formal del Sprint 2
sigue pendiente; este documento no la sustituye ni inventa una retrospectiva.

## S2-01 — Catálogo, búsqueda y ficha

Fechas observables: 12 y 13 de noviembre de 2026.

- Integración de TMDB con búsqueda paginada y consulta de detalle.
- Buscador y ficha visual de películas.
- Contrato normalizado con estados de carga, error y reintento.
- Verificación de integración y documentación de pruebas.

Evidencia: `39c465f`, `0b7bd59`, `6de51bd`,
[docs/sprint2/S2-01-T01-fuente-datos.md](sprint2/S2-01-T01-fuente-datos.md) y
[docs/sprint2/S2-01-T06-pruebas-catalogo.md](sprint2/S2-01-T06-pruebas-catalogo.md).

## S2-02 — Plataformas y disponibilidad

Fechas observables: 12 y 13 de noviembre de 2026.

- Catálogo de plataformas de streaming para España.
- Preferencias por cuenta con selección vacía válida.
- Persistencia y API de preferencias.
- Selector visual y disponibilidad en la ficha.
- Separación de suscripción, alquiler, compra, gratis y anuncios.
- Pruebas de preferencias, permisos y disponibilidad.

Evidencia: `3a9dbee`, `5632fe7`,
[docs/sprint2/S2-02-T01-disponibilidad-region.md](sprint2/S2-02-T01-disponibilidad-region.md),
[docs/sprint2/S2-02-T03-api-preferencias.md](sprint2/S2-02-T03-api-preferencias.md) y
[docs/sprint2/S2-02-T06-pruebas-preferencias.md](sprint2/S2-02-T06-pruebas-preferencias.md).

## Prototipo y mejora de interfaz

Fecha observable: 13 de noviembre de 2026.

La rama `sprint2/hito1-actualizacion-readme-interfaz` reordena la presentación
sin cambiar IDs, contratos de API, permisos ni comportamiento del cliente.
Letterboxd y JustWatch se citan solo como referencias visuales, sin integración
ni copia de datos. Se mantienen los criterios responsive, contraste, foco,
navegación por teclado y `prefers-reduced-motion`.

Evidencia: `125c209`, merge `234640e` y la sección de interfaz del
[README](../README.md).

## Logos de proveedores

Fecha observable: 22 de noviembre de 2026.

El commit `12606d7` muestra el logo de las plataformas en la ficha y en el
selector cuando TMDB lo facilita. El PR #23 se registra fusionado el 24 de
noviembre.

## Resultado y límites

- La suite histórica del Sprint 2 se registra con 229/229 pruebas generales y
  13/13 pruebas de PostgreSQL en la documentación de S2-02-T06.
- La memoria formal del Sprint 2 sigue pendiente. Los documentos por tarea son
  la evidencia disponible.
- No se verificaron en esa revisión OAuth real, entrega real de correo ni un
  despliegue nuevo; esas comprobaciones no se atribuyen al agente.
- La disponibilidad se limita a TMDB para España y no promete tiempo real ni
  reproducción.
