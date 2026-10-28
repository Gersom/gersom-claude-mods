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

Tarea 32 — Mejoras de UX en agent-radar

Tarea chica, sin plan. Alcance final acordado con el operador (2026-10-27): solo cambiar el botón `[ ● Agent Radar: ON ]` a `[ ● ON ]` / `[ ● OFF ]`; el borde y el espacio de la banda quedan **descartados**. Hecho en el mod `agent-radar` (commit `feat(T-32): shorten the ON/OFF button to just ON or OFF`): `buttonLabel`, tests y README. Los avisos (toasts) siguen diciendo `Agent Radar: ON/OFF`. Los 3 tests que fallan ya fallaban antes (kit 2.1.310).

**Próximo paso concreto:** el operador prueba a mano y pide cerrar la tarea (Regla 6); al cerrar, en `history.md` registrar que el borde se descartó.

Última cerrada: Tarea 44. Backlog: Tareas 41 y 43 libres; la 42 bloqueada por la 41.

<!-- agent-context-skill:section=paused -->
## Tareas pausadas

Ninguna
