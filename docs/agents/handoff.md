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

Descripción: que `usage-meter` muestre sus textos (títulos, `Restablece en`, `Categorías`, `Compactar`, `Una línea`, días y meses, `Libre`, `Búfer`…) en más de un idioma, hoy solo en español.

### Plan (pendiente de aprobación del operador)

- [ ] 1. `hooks/i18n.ts`: diccionarios por idioma (`es`, `en`) con todas las cadenas visibles, `detectLang` (puro) y los tipos en `types/index.d.ts`.
- [ ] 2. `format.ts`: las funciones que escriben texto (etiquetas, `relative`, `compactRelative`, fechas, `resetText`, `tokensText`, nombres de leyenda) reciben los textos del idioma en vez de tenerlos fijos.
- [ ] 3. `register.tsx`: leer el idioma al iniciar la sesión (`atom` `lang`) y pasarlo al dibujar; botones y textos sueltos salen del diccionario.
- [ ] 4. Tests (cada idioma) y README.
- [ ] 5. Documentar cierre de tarea (solo cuando el operador lo pida).

Próximo paso: el operador responde las decisiones abiertas y aprueba el plan; luego, paso 1.

Hallazgos verificados en los tipos de la API (`types/claude-code/index.d.ts`): no hay una API de `locale` ni de idioma de la interfaz. Sí hay `$.settings.read()` (la clave `language` de `settings.json`, si el operador la tiene; `3563`) y `$.env.get('LANG')` (nombre literal; `3588`). Sin verificar: qué valores trae `language` en la práctica (¿`spanish`, `español`, `es`?) y si `LANG` existe en Windows.

Última cerrada: Tarea 9 (limpia de código muerto). Backlog: Tareas 11 a 16 (14 y 16 bloqueadas).

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
