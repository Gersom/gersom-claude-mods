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

Tarea 5 — cambiar porcentajes

Mod: `mods/usage-meter`. Rama: `feat/cambiar-porcentajes`, creada desde `feat/cambiar-diseno` (la Tarea 4 aún no está en `main`).

Umbrales nuevos: verde hasta 60 %, amarillo de 61 a 80 %, rojo por encima de 80 %. Interpretación del 80 %: amarillo (confirmar si el operador prefiere rojo).

Pasos:
- [x] Cambiar `level` en `format.ts` y su test.
- [x] Actualizar la sección de umbrales del README.
- [x] `claude plugin validate` pasó; `claude plugin test` 23/23.
- [ ] Revisión en sesión y cierre (pendiente de pedido del operador).

Próximo paso concreto: confirmar el 80 % y revisar en sesión.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
