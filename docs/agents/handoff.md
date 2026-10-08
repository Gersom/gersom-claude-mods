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

Tarea 3 — Construir el primer mod

Implementar `usage-meter` según [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md). El código vive en `mods/usage-meter/` y se carga con `claude --plugin-dir`.

### Plan

- [x] Paso 1 — Estructura base del plugin: `.claude-plugin/plugin.json`, `hooks/hooks.json`, `hooks/register.tsx` y contrato `types/index.d.ts`
- [x] Paso 2 — Lógica pura con tests (barra, color por umbral, tiempo relativo y fecha de restablecimiento)
- [x] Paso 3 — Hook `session.measure` que guarda los datos y `ui.render` en `AbovePrompt` que dibuja el recuadro
- [x] Paso 4 — Validar: `claude plugin validate`, `tsc` y `claude plugin test`
- [ ] Paso 5 — Probar en vivo con `--plugin-dir` y ajustar (terminales angostas): pendiente de la revisión visual del operador
- [ ] Documentar cierre de tarea

**Modo de ejecución acordado:** todos los pasos seguidos

### Qué falta

Paso 5: que el operador cargue el mod en una sesión real (`claude --plugin-dir mods/usage-meter`), revise cómo se ve el recuadro y pida ajustes; luego el cierre (Regla 5).

### Decisiones a medio camino

- Verificado sin sesión interactiva: `claude plugin validate` OK, `tsc` limpio, 16 tests pasan (lógica y render en terminal y desktop con datos simulados).
- El título «Uso» va como fila dentro del recuadro, no en el borde (limitación del `Box`); anotado en el README del mod.

### Próximo paso concreto

Pedirle al operador que pruebe el mod en vivo y reporte ajustes.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
