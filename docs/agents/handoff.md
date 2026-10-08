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

Tarea 2 — Definir de qué trata el primer mod

Definir el primer mod y documentarlo en `mods/<nombre>/README.md` (convención en el [`README.md`](../../README.md) raíz). Hecho: [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md) escrito como borrador.

### Qué falta

Que el operador revise la definición y pida cerrar la tarea (Regla 5 de `rules.md`).

### Decisiones a medio camino

- Primer mod: `usage-meter`, un hook que muestra en un recuadro solo el % de contexto, de la ventana de 5 horas y de la semanal.
- Factible con la API actual: evento `session.measure` (contexto + `rateLimits`) y render en `AbovePrompt`.
- Abierto: formato visual del recuadro; "uso del plan" se toma como las ventanas de 5h y semanal.

### Próximo paso concreto

Esperar la revisión del operador; al pedir el cierre, documentar en `history.md` y `backlog.md`.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
