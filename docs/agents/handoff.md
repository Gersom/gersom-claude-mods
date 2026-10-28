<!-- agent-context-skill:signature — ignorar al leer/actualizar este archivo, no es contenido. Existe solo para identificar que fue generado por https://github.com/Gersom/agent-context-kit, útil para el flujo de migración (ver skill/docs/migration-flow.md) cuando hay que distinguir este skill de un sistema de documentación parecido pero distinto. Opcional: su ausencia no significa que el archivo no sea de este skill. -->

# Handoff

Estado "en caliente": en qué se está ahora. **Se sobrescribe completo** en cada actualización (en cada paso del plan y al cerrar la tarea): es una foto del presente, no un historial, con el próximo paso concreto para que un chat nuevo retome sin depender de la sesión anterior.

- Pendientes → [`./backlog.md`](./backlog.md) · Cerradas (hechas o descartadas) → [`./history.md`](./history.md)
- Sin tarea en curso: "Tarea en progreso" dice "Sin tarea en curso" (no deja el contenido de la última cerrada); "Tareas pausadas" queda en "Ninguna" si no hay.
- **No borres ni muevas los comentarios `<!-- agent-context-skill:section=... -->`** (`in-progress`, `paused`): los lee el script de seguimiento de tareas; como el archivo se reescribe completo, hay que reescribirlos siempre. La tarea en curso va en una línea `Tarea N — título` antes de la primera subsección `###`.
- **Tarea pausada:** un bloque `### Tarea N — título` con `Plan` (opcional: los checkboxes de "Tarea en progreso" tal cual), `Qué falta`, `Decisiones a medio camino`, `Próximo paso concreto`, `Por qué se pausó` y `Qué espera para retomarse`.
- Las reglas para cerrar una tarea están al final de [`rules.md`](./rules.md).

---

<!-- agent-context-skill:section=in-progress -->
## Tarea en progreso

Tarea 44 — Renombrar «Claude Radar» a «Agent Radar» en la pantalla

Tarea chica, sin plan. Hecha en el mod `agent-radar` (commit `feat(T-44): rename the visible title to Agent Radar`): `NAME`, textos de los botones, avisos y descripción del comando, tests y README. El archivo `hooks/claude-radar.tsx` y `docs/claude-radar.md` conservan su nombre; las entradas de `history.md` no se tocaron (son historia). Los 3 tests que fallan ya fallaban antes (kit 2.1.310).

**Próximo paso concreto:** el operador prueba a mano y pide cerrar la tarea (Regla 6).

Última cerrada: Tarea 31 (descartada). Backlog: Tareas 32, 41 y 43 libres; la 42 bloqueada por la 41.

<!-- agent-context-skill:section=paused -->
## Tareas pausadas

Ninguna
