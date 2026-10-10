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

Tarea 19 — Crear repo hijo usage-meter

Sacar `mods/usage-meter` a su propio repo `Gersom/claude-mod-usage-meter`, con su `.git` dentro de `mods/usage-meter/` y el central dejando de versionarlo. Plan aprobado por el operador; ejecutado seguido (pasos 1 a 6).

### Plan

- [x] 1. Extraer el historial del mod (25 commits) con `git subtree split --prefix=mods/usage-meter` a una rama temporal del central.
- [x] 2. Crear el repo remoto `Gersom/claude-mod-usage-meter` con `gh` (público; el operador lo autorizó).
- [x] 3. Inicializar el repo del mod: mover los archivos a un repo con su `.git` en `mods/usage-meter/`, con el historial extraído, y subirlo a `origin` del mod.
- [x] 4. Llevar al `.gitignore` del mod las entradas que hoy tiene el central: `tsconfig.json` y `.claude-plugin/types/`.
- [x] 5. En el central: `git rm --cached -r mods/usage-meter` (los archivos quedan en disco) y borrar la rama temporal.
- [x] 6. Verificar que `mods/usage-meter` es un repo propio y que `git status` del central ya no lo ve; correr los tests del mod.
- [ ] 7. Documentar cierre de tarea (solo si el operador lo pide).

Próximo paso concreto: paso 7, documentar el cierre, solo cuando el operador lo pida. Pasos 1 a 6 hechos: repo `Gersom/claude-mod-usage-meter` (público, 26 commits en `origin/main`: los 25 del mod más el `.gitignore`), 63 tests pasan, el central ya no versiona el mod.

Tareas siguientes: 20 (preparar el repo de `usage-meter`; bloqueada por la 19) y 12 (publicar; bloqueada por 19 y 20). Backlog libre: 13, 15 y 21; 14, 16, 20 y 12 bloqueadas.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
