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

Tarea 13 — Iniciar nuevo mod para mostrar el caché

Decisiones del operador: mod aparte con su propio panel, nombre `cache-watch` (deja espacio a más datos), pasos ejecutados seguidos. Objetivo: mostrar si el caché de prompts está caliente o frío (cuenta regresiva hasta que se enfríe; frío = la próxima petición reescribe toda la conversación).

Hallazgos del paso 1: el motor no expone el TTL (`5m`/`1h`) a los hooks de plugin ni la hora de la última respuesta; el TTL va como opción `userConfig` (por defecto `1h`) y la hora se toma de `session.measure`/`turn.step`/`turn.complete` del hilo principal. Panel = banda `AbovePrompt`, envolviendo lo que devuelva `next(e)` para convivir con `usage-meter`.

- [x] 1. Cargar `plugin-authoring` y verificar los datos de caché disponibles
- [x] 2. Diseño fijado (arriba)
- [ ] 3–4. Crear `mods/cache-watch/` (repo propio) con código, tests y README
- [ ] 5. Verificar (`claude plugin validate` / `claude plugin test`)
- [ ] 6. Publicar: repo `Gersom/claude-mod-cache-watch` y entrada en `.claude-plugin/marketplace.json`
- [ ] 7. Documentar cierre de tarea (solo cuando el operador lo pida)

Próximo paso: delegar a ᴇsᴄʀɪᴛᴏʀ la creación del mod (pasos 3–4).

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
