# Requisitos documentales

Estado de las fuentes: 25 de noviembre de 2026.

Los identificadores `CM-RF-xx` son propios de esta documentación de CineMatch.
No son identificadores de DoneTonic ni del profesorado, no reproducen su
numeración y no sustituyen a los requisitos de la asignatura. La evidencia se
limita a rutas y pruebas presentes en esta rama.

## Requisitos implementados

| ID | Requisito | Evidencia principal |
|---|---|---|
| CM-RF-01 | Registro local con cuenta pendiente y confirmación por correo. | `test/registro.test.js`, `test/confirmacion.test.js`, `sql/004-confirmacion-correo.sql`. |
| CM-RF-02 | Login, sesión de 8 horas, logout y perfil propio. | `test/autenticacion.test.js`, `test/api-sesiones.test.js`, `test/api-perfil.test.js`. |
| CM-RF-03 | Acceso con Google OAuth/OpenID Connect sin exponer tokens al cliente. | `test/oauth.test.js`, `test/oauth-concurrencia.test.js`, `Servidor/google-oauth.js`. |
| CM-RF-04 | Baja lógica propia y reutilización posterior del correo. | `test/cuentas-reutilizables.test.js`, `sql/005-correos-disponibles.sql`. |
| CM-RF-05 | Roles `usuario` y `administrador` con autorización en servidor. | `test/roles.test.js`, `test/api-usuarios.test.js`, `sql/002-roles.sql`. |
| CM-RF-06 | Búsqueda de películas en TMDB con paginación y contrato normalizado. | `test/api-peliculas.test.js`, `test/busqueda-peliculas.test.js`, `test/catalogo-tmdb.test.js`. |
| CM-RF-07 | Ficha de película con datos normalizados y estados de error. | `test/api-detalle-pelicula.test.js`, `test/detalle-pelicula.test.js`, `test/catalogo-cliente.test.js`. |
| CM-RF-08 | Catálogo de plataformas para España y preferencias por cuenta. | `test/api-preferencias.test.js`, `test/preferencias-plataformas.test.js`, `test/selector-plataformas.test.js`. |
| CM-RF-09 | Disponibilidad en España separada por tipo y sin inventar datos. | `test/api-disponibilidad.test.js`, `test/disponibilidad-pelicula.test.js`, `test/disponibilidad-cliente.test.js`. |
| CM-RF-10 | Recuperación de contraseña local con token de un solo uso. | `test/api-recuperacion.test.js`, `test/recuperacion.test.js`, `test/passwords.test.js`. |
| CM-RF-11 | Logs JSON sin secretos, cookies, tokens ni cuerpos. | `test/actividad.test.js`, `Servidor/actividad.js`. |
| CM-RF-12 | Persistencia PostgreSQL con migraciones 001–006 y 008. | `test/estructura.test.js`, `integracion/postgres.js`, `integracion/recuperacion-postgres.js`. |
| CM-RF-13 | Preferencias y disponibilidad con PostgreSQL real. | `integracion/preferencias-postgres.js`, `integracion/api-preferencias-postgres.js`, `integracion/api-disponibilidad-postgres.js`. |
| CM-RF-14 | Interfaz responsive, accesible y sin dependencias de cliente. | Validación manual descrita en el [README](../README.md); no hay pruebas que solo inspeccionen CSS. |

## Requisitos pendientes o fuera de alcance

| ID | Requisito | Estado y límite |
|---|---|---|
| CM-RF-15 | Listas personales y su persistencia. | Pendiente. PR #24 cerrado sin integrar y PR #27 abierto; no existe migración 007 ni integración demostrada. |
| CM-RF-16 | Recomendaciones de películas. | Fuera de alcance del Sprint 3; no hay implementación ni datos inventados. |
| CM-RF-17 | Reseñas y valoraciones. | Fuera de alcance; no se generan reseñas ni puntuaciones ficticias. |
| CM-RF-18 | Historial de actividad y funciones sociales. | Fuera de alcance; no hay rutas ni tablas asociadas en esta rama. |

## Criterios de lectura

- Una prueba en `test/` cubre comportamiento en memoria, HTTP o cliente; una
  prueba en `integracion/` requiere PostgreSQL real.
- La presencia de una ruta o tabla no demuestra por sí sola el requisito: se
  exige la prueba o la validación indicada.
- La entrega real de Gmail y el funcionamiento en Cloud Run no están cubiertos
  por la suite. El README registra que esa validación la aporta el responsable
  del proyecto.
- Los requisitos pendientes no se marcan como integrados por existir una rama o
  una PR abierta.
