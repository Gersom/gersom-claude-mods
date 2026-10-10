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

Tarea 18 — Preparar repo central para marketplace

Convertir `claude-mods` en el repo central `Gersom/gersom-claude-mods`. Modo: paso a paso, con confirmación del operador después de cada paso. El operador autorizó expresamente renombrar el repo con `gh` (cuenta `Gersom`).

### Plan

- [x] 1. Cambio de nombre: repo renombrado con `gh` a `Gersom/gersom-claude-mods` y `origin` actualizado a `git@github.com:Gersom/gersom-claude-mods.git` (verificado con `git ls-remote`). Quedan menciones del nombre viejo en `README.md`, `docs/README.md`, `architecture.md` y `package.json` (`name`), que se ajustan en los pasos 4 y 5.
- [x] 2. Ignorar `mods/` en `.gitignore` (el `git rm --cached` de `mods/usage-meter` va en la Tarea 19).
- [x] 3. `.claude-plugin/marketplace.json` con `name: "gersom-claude-mods"`, `owner.name: "Gersom"` y `plugins: []`.
- [x] 4. `README.md` del central con la línea `/plugin marketplace add Gersom/gersom-claude-mods`.
- [x] 5. Actualizar `architecture.md`, `docs/README.md` y la Regla 9 de `rules.md` (commits en varios repos; `mods/` fuera de este repo).
- [x] 6. Validar con `claude plugin validate .`.
- [ ] 7. Documentar cierre de tarea (solo si el operador lo pide).

Próximo paso concreto: paso 7, documentar el cierre, solo cuando el operador lo pida. La validación (`claude plugin validate .`) pasa con un aviso esperado: el catálogo no tiene plugins hasta la Tarea 12.

Pendientes ya creados: Tareas 19 (repo hijo `usage-meter`), 20 (prepararlo; bloqueada por la 19) y 12 (publicar; bloqueada por 18, 19 y 20). Backlog libre: 13, 15 y 19; 14, 16, 20 y 12 bloqueadas.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
