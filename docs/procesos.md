# Procesos de trabajo

Estado de las fuentes: 25 de noviembre de 2026. El protocolo completo vive en
[AGENTS](../AGENTS.md); este documento resume el flujo observable.

## Roles

| Rol | Responsabilidad |
|---|---|
| ChatGPT | Arquitecto y revisor: contratos, criterios de aceptación, seguridad, autorización, casos límite y bugs difíciles. No escribe código salvo escalado. |
| opencode | Implementa código, pruebas, refactors mecánicos y documentación. Lee el diff y ejecuta las pruebas acordadas. |
| Ollama local | Tareas mecánicas y repetitivas. No decide diseño, seguridad ni rendimiento. |
| Responsable del proyecto | Aclara requisitos, valida el producto, crea el commit, hace push, abre la PR y decide la fusión. |

El agente no hace commit, push, PR ni merge por iniciativa propia. Tampoco debe
publicar credenciales, tokens ni datos personales en el repositorio o en los
logs.

## Flujo de una tarea

1. ChatGPT entrega una especificación breve: objetivo, archivos exactos,
   criterio verificable, restricciones y pseudocódigo solo si hace falta.
2. opencode implementa y actualiza pruebas o documentación.
3. opencode devuelve el diff, un resumen máximo de cinco líneas y la salida de
   las pruebas que correspondan.
4. ChatGPT revisa solo el diff y los resultados. Los comentarios usan el formato
   `archivo:línea → problema → cambio esperado`.
5. El responsable del proyecto revisa, hace commit, push, abre la PR y fusiona
   cuando el estado es aceptable.
6. GitHub Actions valida la PR antes de la fusión.

Si opencode falla dos veces la misma tarea, ChatGPT escribe la parte crítica o
da pseudocódigo exacto y opencode lo integra. Sin pruebas en verde no hay
revisión del modelo grande.

## Integración continua

`.github/workflows/ci.yml` se activa en pull requests hacia `main` y en pushes a
`main` y a las ramas históricas enumeradas. El job `pruebas` usa PostgreSQL 17,
Node.js 24 y credenciales ficticias.

Pasos observables:

1. Descargar el código e instalar con `npm ci`.
2. Aplicar `sql/001-usuarios.sql` a `sql/006-preferencias-plataformas.sql` y
   `sql/008-recuperacion-password.sql`, en ese orden.
3. Ejecutar `npm test`.
4. Ejecutar `npm run test:postgres`.

No existe el paso 007 en esta rama. El CI no despliega: la construcción y el
despliegue se describen en el README como responsabilidad de Cloud Build, fuera
del workflow de GitHub Actions.

## Reglas de seguridad y datos

- SQL siempre parametrizado; migraciones aplicadas en orden.
- Secretos solo en `.env` local, Cloud Run o Secret Manager; `.env.example`
  contiene nombres y ejemplos, nunca valores reales.
- El navegador no recibe tokens de TMDB, SMTP, OAuth ni Google.
- Logs JSON con campos cerrados y sin consultas, cuerpos, cookies, tokens,
  contraseñas, correos ni mensajes crudos de proveedores.
- Las pruebas usan datos ficticios y bases exclusivas; no se ejecutan contra
  producción ni contra Gmail real.
- La documentación distingue hechos comprobados, inferencias y validaciones
  manuales del responsable del proyecto.
