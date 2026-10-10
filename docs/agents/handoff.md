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

Tarea 20 — Preparar repo usage-meter para el marketplace

Dejar `Gersom/claude-mod-usage-meter` (en `mods/usage-meter/`) listo para publicarse. Plan aprobado por el operador; ejecutado seguido (pasos 1 a 6), con el plugin en la raíz del repo (`source: "./"`).

### Plan

- [x] 1. `LICENSE` MIT (Gersom, 2026) en el repo del mod.
- [x] 2. `plugin.json`: `version: "1.0.0"`, `license: "MIT"`, `repository` y `homepage` (`https://github.com/Gersom/claude-mod-usage-meter`).
- [x] 3. `.claude-plugin/marketplace.json` del mod, con una entrada (`source: "./"`, por verificar con el validador), para instalarlo suelto.
- [x] 4. README: línea de instalación (`/plugin install usage-meter --marketplace Gersom/claude-mod-usage-meter`), requisito de Claude Code 2.1.287+, licencia y, si el operador lo quiere, enlace de donación.
- [x] 5. Validar (`claude plugin validate .` y `--strict`) y correr los tests.
- [x] 6. Commits y `push` del repo del mod; los docs de la tarea, en el central.
- [ ] 7. Documentar cierre de tarea (solo si el operador lo pide).

Próximo paso concreto: paso 7, documentar el cierre, solo cuando el operador lo pida. Hecho: `LICENSE` MIT, `plugin.json` 1.0.0 con `license`/`repository`/`homepage`, `.claude-plugin/marketplace.json` (`source: "./"` valida), README con instalación, licencia y PayPal; `validate` y `--strict` pasan, 63 tests, y push del repo del mod hecho (`3ebd699`, `6a565b9`). No se probó instalar desde GitHub en una sesión real.

Backlog: Tareas 13, 15 y 21 libres; 14, 16 y 12 bloqueadas (por 13, 15 y 20).

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
