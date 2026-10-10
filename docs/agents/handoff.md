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

Tarea 10 — Multi idioma para usage-meter

Descripción: que `usage-meter` muestre sus textos en español e inglés según `settings.language`, sin que ningún agente ni subagente traduzca nada (diccionarios fijos en el mod, sin llamadas a modelos ni tokens).

Decisiones del operador: idiomas español e inglés; **por defecto, inglés** si no se detecta; automático por `settings.language` y además un botón `[ES]`/`[EN]` para cambiarlo a mano (no persiste: al reiniciar vuelve al automático; la persistencia con `$.store` no se pidió y no se hizo).

### Plan (aprobado; ejecución seguida)

- [x] 1. `hooks/i18n.ts` (diccionarios `es`/`en`, `detectLang`, `otherLang`, `DEFAULT_LANG = 'en'`) y tipos `Lang` y `lang` en `types/index.d.ts`.
- [x] 2. `format.ts`: las funciones que escriben texto reciben `Texts` por parámetro (`rowsOf`, `rowOf`, `contextRow`, `resetText`, `relative`, `shortDate`, `longDate`, `tokensText`, `slicesOf`).
- [x] 3. `register.tsx`: `atom` `lang` (`null` hasta leerlo); `ensureLang` lee `$.settings.read()` en `session.start` y `session.measure`; botón `[ES]`/`[EN]` al pie; botones y `Categorías` salen del diccionario.
- [x] 4. Tests (63/63, validación OK, sin verificar a mano en la app) y README (sección «Idioma»).
- [ ] 5. Documentar cierre de tarea (solo cuando el operador lo pida).

Verificado: `settings.language` es texto libre (el esquema oficial de `settings.json` lo describe con ejemplos en inglés: `japanese`, `spanish`, `french`) y el del operador es `"Español"` (`~/.claude/settings.json`, línea 21), por eso `detectLang` ignora mayúsculas y tildes y reconoce `es`, `es-MX`, `spanish`, `castellano`; un idioma como `Estonian` no se confunde con español (se compara la primera palabra entera). `claude plugin validate` lista las llamadas del mod: reloj, `session.usage`, `settings.read`, estado y UI; ninguna a modelos. Sin verificar: que `$.settings.read()` en una sesión real devuelva `language` fusionado (solo probado con el mock de los tests).

Próximo paso: el operador lo prueba en sesión real (`bun run usage-meter`; con su configuración debería salir en español) y pide cerrar la tarea.

Última cerrada: Tarea 9 (limpia de código muerto). Backlog: Tareas 11 a 16 (14 y 16 bloqueadas).

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
