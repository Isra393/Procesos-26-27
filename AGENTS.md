# AGENTS.md — CineMatch

Guía para agentes de IA que trabajen en este repositorio y protocolo de
colaboración entre el modelo grande de revisión (ChatGPT) y opencode.

## Contexto del proyecto

- Asignatura: Procesos de la Ingeniería del Software. Sprint 3 en curso.
- Producto: CineMatch, catálogo y disponibilidad de películas (TMDB, región ES).
- Stack: Node.js `>=24.19.0 <25` con módulos ES, HTTP nativo de Node.js,
  PostgreSQL 17 con `pg`, cliente HTML/CSS/JS sin framework y `node:test`.
- Alcance Sprint 3: recuperación de contraseña local ya integrada y seguimiento
  de listas pendiente. Recomendaciones, reseñas, valoraciones, historial y
  funciones sociales siguen fuera de alcance.
- No se inventan películas, valoraciones, recomendaciones ni enlaces de
  proveedores. La disponibilidad se limita a la información de TMDB para ES.
- Documentación general: `docs/index.md`; documentación de sprint:
  `docs/sprint2/` y `docs/sprint3/`.
- Repositorio: <https://github.com/chemaa14/Procesos-26-27>

## Estado de Sprint 3

- Recuperación de contraseña local (#25) integrada mediante el PR #26 fusionado
  y migración `sql/008-recuperacion-password.sql`.
- Listas: el PR #24 está cerrado sin integrar y el PR #27 sigue abierto y
  pendiente. No afirmar la integración de listas ni que la migración 007 esté
  aplicada: no existe 007 en esta rama.
- Evidencias y seguimiento semanal en `docs/sprint3/semana-1.md`.

## Comandos

| Acción | Comando |
|---|---|
| Instalar dependencias | `npm.cmd ci` |
| Base de datos local | `docker compose up -d --wait` |
| Arrancar con PostgreSQL | `npm.cmd run start:postgres` |
| Pruebas unitarias, HTTP y en memoria | `npm.cmd test` |
| Pruebas con PostgreSQL real | `npm.cmd run test:postgres` |
| CI | GitHub Actions ejecuta ambos comandos en cada PR hacia `main` |

`npm.cmd test` no requiere PostgreSQL, TMDB, Gmail ni credenciales.
`npm.cmd run test:postgres` requiere una base exclusiva con las migraciones
001 a 006 y 008 aplicadas según el `package.json` actual (no existe 007 en esta
rama; ver `README.md`).

## Convenciones

- No añadir frameworks ni dependencias de cliente; el CSS vive en
  `Cliente/estilos.css` y se sirve desde el mismo backend.
- API y frontend en el mismo origen. El navegador nunca recibe secretos
  (TMDB, SMTP, OAuth ni tokens de Google).
- SQL siempre parametrizado; migraciones en `sql/` aplicadas en orden.
- Textos de usuario con `textContent`; validar y normalizar en el cliente.
- Logs JSON con campos cerrados y sin secretos ni tokens.
- `.env` no se versiona; `.env.example` solo contiene nombres y ejemplos.
- Pruebas con `node:test` y `node:assert/strict`; no añadir pruebas que solo
  inspeccionen CSS.
- Un cambio no está terminado sin pruebas nuevas o actualizadas y sin
  `npm.cmd test` en verde.

## Protocolo de trabajo conjunto

### Roles

- **ChatGPT (modelo grande):** arquitecto y revisor. Define contratos,
  criterios de aceptación, seguridad, autorización, casos límite y bugs
  difíciles. No escribe código salvo que opencode falle dos veces la misma
  tarea.
- **opencode (modelo pequeño/local):** implementa código, pruebas, refactors
  mecánicos y documentación.
- **Ollama local (`qwen2.5-coder:7b/14b`):** tareas mecánicas y repetitivas
  (boilerplate, renombrados, pruebas triviales, docs). Diseño, seguridad y
  rendimiento no se delegan a local.

### Cómo pide el trabajo ChatGPT

Una especificación por tarea, con este formato:

1. **Objetivo:** qué debe funcionar al terminar.
2. **Archivos exactos a tocar:** rutas concretas, sin volcar el repositorio.
3. **Criterio de aceptación verificable:** pruebas que deben pasar.
4. **Restricciones:** contratos que se mantienen, zonas que no se tocan.
5. **Pseudocódigo:** solo si hay una decisión no obvia que explicar.

No reenviar archivos completos ni contexto ya conocido. Rutas y fragmentos
mínimos.

### Qué devuelve opencode

- El diff de los cambios.
- Un resumen de cinco líneas como máximo.
- La salida de `npm.cmd test` y, si aplica, `npm.cmd run test:postgres`.
- Si algo falla, el error exacto y la prueba afectada.

### Cómo revisa ChatGPT

- Revisa solo el diff y los resultados de las pruebas, no archivos enteros.
- Comentarios accionables en formato `archivo:línea → problema → cambio
  esperado`.
- Una sola ronda de revisión por tarea. Si hacen falta más, la especificación
  estaba mal y se reescribe.

### Contexto y optimización de tokens

- Mantener al inicio de la conversación un bloque fijo con stack,
  convenciones, estado del sprint y comandos. No repetirlo en cada mensaje;
  actualizarlo solo cuando cambie.
- Leer solo lo necesario (búsquedas y fragmentos), no el repositorio completo.
- En opencode, usar `/compact` si la sesión crece y `/export` para archivar la
  conversación.
- El modelo grande se reserva para diseño, seguridad, autorización y bugs
  sutiles.

### Escalado

- Si opencode falla dos veces la misma tarea, ChatGPT escribe la parte crítica
  (o da pseudocódigo exacto) y opencode la integra.
- Sin pruebas que pasen, no hay revisión del modelo grande.

### Regla de oro

ChatGPT piensa, opencode pica, los tests deciden.
