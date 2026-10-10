<!-- agent-context-kit:signature — ignorar al leer/actualizar este archivo, no es contenido. Existe solo para identificar que fue generado por https://github.com/Gersom/agent-context-kit, útil para el flujo de migración (ver skill/docs/migration-flow.md) cuando hay que distinguir este skill de un sistema de documentación parecido pero distinto. Opcional: su ausencia no significa que el archivo no sea de este skill. -->

# Handoff

Estado "en caliente": en qué se está ahora. **Se sobrescribe completo** en cada actualización (en cada paso del plan y al cerrar la tarea): es una foto del presente, no un historial, con el próximo paso concreto para que un chat nuevo retome sin depender de la sesión anterior.

- Pendientes → [`./backlog.md`](./backlog.md) · Cerradas (hechas o descartadas) → [`./history.md`](./history.md)
- Sin tarea en curso: "Tarea en progreso" dice "Sin tarea en curso" (no deja el contenido de la última cerrada); "Tareas pausadas" queda en "Ninguna" si no hay.
- **No borres ni muevas los comentarios `<!-- agent-context-kit:section=... -->`** (`in-progress`, `paused`): los lee el script de seguimiento de tareas; como el archivo se reescribe completo, hay que reescribirlos siempre. La tarea en curso va en una línea `Tarea N — título` antes de la primera subsección `###`.
- **Tarea pausada:** un bloque `### Tarea N — título` con `Plan` (opcional: los checkboxes de "Tarea en progreso" tal cual), `Qué falta`, `Decisiones a medio camino`, `Próximo paso concreto`, `Por qué se pausó` y `Qué espera para retomarse`.
- Las reglas para cerrar una tarea están al final de [`rules.md`](./rules.md).

---

<!-- agent-context-kit:section=in-progress -->
## Tarea en progreso

Tarea 8 — Añadir categorías al contexto

Descripción: en la fila de Contexto de `usage-meter`, mostrar el desglose por categorías (prompt del sistema, herramientas, MCP, agentes, memoria, skills, mensajes, libre) como en el `/context` de Claude Code. Sale de la Tarea 6.

### Plan (aprobado; `breakdown: 'summary'`; ejecución seguida)

- [x] 1. Obtener el desglose: `$.session.usage({ breakdown: 'summary' })` al iniciar y en cada `session.measure`; categorías (nombre, tokens, `kind`) en `Usage.context.categories`. Si falla, queda vacío.
- [x] 2. Dibujarlo: barra segmentada a todo el ancho y leyenda (`slicesOf` en `format.ts`), con paleta propia (la API da el color como clave de tema, no hex), debajo de la fila de Contexto.
- [x] 3. Tests (34/34, validación OK) y README.
- [ ] 4. Documentar cierre de tarea.

Próximo paso: el operador revisa en sesión real (`bun run usage-meter`; no verificado a mano) y pide cerrar; entonces, el paso 4. La fila de Contexto queda con su barra de 10 celdas y además la segmentada: redundante, candidato para la Tarea 7 (UX).

Verificado: `session.measure` NO trae el desglose (solo `tokens`, `window`, `percent`). Sí lo trae `$.session.usage({ breakdown })` (`types/claude-code/index.d.ts:2825`), en `context.breakdown.categories` (`ContextCategory`: `name`, `tokens`, `kind` = `used | free | buffer | deferred`, `color` como clave de tema). `'summary'` estima en local y no cuesta; `'full'` usa la API de conteo de tokens. Sin verificar: si llamarlo en cada medición es lo bastante barato.

Última cerrada: Tarea 6 (tokens en el contexto). Backlog: Tarea 7 (mejorar la UX).

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
