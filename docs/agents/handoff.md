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

Tarea 6 — Añadir tokens al contexto (las categorías pasaron a la Tarea 8)

### Plan (aprobado; ejecución seguida)

- [x] 1. Ampliar `Usage.context` a `{ percent, tokens, window }` (`types/index.d.ts`, `register.tsx`, `contextRow` en `format.ts`).
- [x] 2. Mostrar en la fila de contexto `84k de 200k` (`compactTokens` y `tokensText` en `format.ts`), en gris atenuado tras el porcentaje.
- [x] 3. Tests (27/27, validación OK) y README.
- [ ] 4. Documentar cierre de tarea.

Próximo paso: el operador revisa el resultado (sesión real con `bun run usage-meter`, no verificado a mano) y pide cerrar la tarea; entonces, el paso 4.

Última cerrada: Tarea 5 (umbrales de color a 60 y 80). Backlog: Tareas 7 (mejorar la UX) y 8 (categorías del contexto).

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
