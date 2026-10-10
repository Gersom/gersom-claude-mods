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

Tarea 7 — Mejorar la UX

Descripción: mejorar la experiencia visual y de uso del panel de `usage-meter`. Punto de partida: acercar el diseño a la captura de `/context` que adjuntó el operador (recuadro con `◆` y título en negrita, recuadro de porcentaje con color de umbral, barra a todo el ancho con la parte vacía en gris oscuro).

Alcance elegido por el operador: cabecera estilo captura, una sola barra por medida, leyenda en columnas y separación entre medidas. Cuando lo vea aplicado dirá si hay que cambiar algo más.

### Plan (aprobado; ejecución seguida)

- [x] 1. `format.ts`: `barParts` con ancho variable, `percentBadge` (` 42% `), `head`/`inlineFits` ajustados a la nueva cabecera y `legendRows(slices, columns)` que reparte la leyenda en columnas alineadas.
- [x] 2. `register.tsx`: cabecera con `◆` en el color de la medida, etiqueta en negrita y a la derecha el texto de restablecimiento / tokens y el % como recuadro con fondo del color de umbral; sin título «Uso»; línea en blanco entre medidas.
- [x] 3. `register.tsx`: una sola barra a todo el ancho por medida (vacío en gris oscuro); en Contexto, la segmentada reemplaza a la de 10 celdas, y la leyenda va en columnas.
- [x] 4. Tests (39/39, validación OK) y README (diseño y ejemplo).
- [x] 5. Refinamiento de UX (tests 44/44, validación OK, sin verificar a mano): (a) colores por nombre, `MCP server instructions` naranja y `Messages` violeta; (b) leyenda en el orden `■ nombre % tokens`; (c) texto de las categorías en gris `#9ca3af`; (d) las líneas en blanco entre medidas pasan a tener prioridad sobre la leyenda (antes se quitaban primero, por eso no se veían).
- [ ] 6. Documentar cierre de tarea.

Primera revisión del operador (captura en la app de escritorio) y correcciones aplicadas:
- Faltaban los límites de 5 horas y semanal: causa probable (inferida, no verificada en la app), la franja admite `maxRows` filas y las últimas se desplazan fuera de vista; ahora el reparto prioriza cabeceras y barras, luego la leyenda y al final las líneas en blanco.
- La barra del contexto se partía en dos líneas: eran `Text` con `█` repetido, más anchos que el contenedor real; ahora son `Box` con `flexGrow` proporcional (el motor limita `flexGrow` a 10000).
- La leyenda vuelve a ir seguida, no en columnas.

Próximo paso: el operador vuelve a verlo en sesión real (`bun run usage-meter`), dice si hay que cambiar algo más y pide cerrar; entonces, el paso 6.

Contexto: `Row.bar`, `bar()`, `barParts` y `Slice.cells` ya no se usan al dibujar (solo los tests); se pueden limpiar si el operador lo pide.

Última cerrada: Tarea 8 (categorías del contexto). Backlog sin tareas libres.

<!-- agent-context-kit:section=paused -->
## Tareas pausadas

Ninguna
