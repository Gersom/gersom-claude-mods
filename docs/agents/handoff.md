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

Tarea 12 — Subir el mod usage-meter al marketplace

Publicar `usage-meter` en el catálogo del central (`Gersom/gersom-claude-mods`). Plan aprobado; ejecutado seguido.

### Plan

- [x] 1. Agregar la entrada de `usage-meter` a `.claude-plugin/marketplace.json` del central, con `source: {source: "github", repo: "Gersom/claude-mod-usage-meter"}`.
- [x] 2. Actualizar la tabla «Mods» del `README.md` del central (nombre, qué hace, repo).
- [x] 3. Validar el central con `claude plugin validate .`.
- [x] 4. Commit y `push` del central (el catálogo se lee desde GitHub, así que hay que subirlo para probar).
- [x] 5. Probar la instalación real desde GitHub en una configuración aislada (`CLAUDE_CONFIG_DIR` temporal), sin tocar la del operador: `marketplace add Gersom/gersom-claude-mods` e `install usage-meter@gersom-claude-mods`, y lo mismo con el repo del mod.
- [x] 6. El operador revisa cómo se ve en la app de escritorio (menú de plugins), que no puedo ver desde acá.
- [ ] 7. Documentar cierre de tarea (solo si el operador lo pide).

Próximo paso concreto: paso 7, documentar el cierre, solo cuando lo pida. Hecho: entrada de `usage-meter` en el catálogo (commit `feat(T-12)`, con push) y README del central; `validate` pasa. El operador verificó la app de escritorio (aparece en Plugins → Descubrir con el filtro Origen) y las instrucciones quedaron en los README. Instalación real probada en una configuración aislada, sin tocar la del operador: el central (`install usage-meter@gersom-claude-mods`) y el repo suelto (`install usage-meter --marketplace Gersom/claude-mod-usage-meter`) instalaron la versión 1.0.0.

Backlog: Tareas 13 y 15 libres; 14 y 16 bloqueadas por 13 y 15.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
