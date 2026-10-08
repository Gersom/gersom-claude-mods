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

Tarea 4 — cambiar diseño

Feature doc: [`odd/tasks/cambiar-diseno.md`](../../odd/tasks/cambiar-diseno.md). Mod: `mods/usage-meter`.

Pasos del plan:
- [x] Mover la tarea del backlog a este archivo y crear el feature doc.
- [ ] `format.ts`: funciones de presentación (bloques vacíos en gris, porcentaje alineado, reset atenuado). Sin cambiar cálculos.
- [ ] `register.tsx`: layout nuevo (título `Uso` gris suave, etiquetas y barra en color distintivo, reset en segunda línea en terminales estrechas).
- [ ] Animación: valor mostrado en `$.state`, `$.clock.every` que avanza hacia el objetivo; durante la animación la barra va en color distintivo y al terminar vuelve al color del umbral.
- [ ] Tests y validación (`claude plugin test mods/usage-meter`, `claude plugin validate mods/usage-meter`).
- [ ] Documentar cierre (README, history).

Decisiones tomadas:
- Etiquetas y barra con color distintivo: `Contexto` en azul; `5 horas` y `Semana` en violeta (la especificación da verde o violeta; se eligió violeta para no confundirlo con el verde del umbral).
- Barra en reposo: color del umbral. En animación: color distintivo, y luego vuelve al del umbral.
- Terminal estrecha: reset en segunda línea.
- Solo tema oscuro; no se contempla el claro.
- Umbrales actuales (70/90) se mantienen en esta tarea; el cambio a 60/80 es la Tarea 5.

Próximo paso concreto: implementar `format.ts` y sus tests.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
