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

Tarea 43 — Pulir usage-meter: tests del panel y tipos

Tarea chica, sin plan. Hecho en el mod `usage-meter` (commit `fix(T-43): clear the type errors of tsc and note what the tests cannot cover`, `d68e6f8`): `bunx tsc --noEmit` ya no da errores (claves de lista `key={`${at}`}`, valores posiblemente `undefined` en `format.ts` y `format.test.ts`); 68 tests pasan.

**No se pudo:** los tests del hook `ui.close` (cierre de la persona) y del orden «`ui.open` primer `await`» en el botón. El arnés de pruebas del motor (`$.ui` solo trae `render`, `scroll`, `focus`, `press`, `input`, `select`, `mount`) no tiene `close` ni deja observar ese orden. Quedó escrito en «Limitaciones conocidas» del README del mod; el test del comando ya cubre el orden para ese camino. Al cerrar, registrarlo así en `history.md`.

**Próximo paso concreto:** el operador pide cerrar la tarea (Regla 6).

Última cerrada: Tarea 41 (descartada). Backlog: Tarea 42 libre.

<!-- agent-context-skill:section=paused -->
## Tareas pausadas

Ninguna
