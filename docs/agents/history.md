# History

Historial de tareas resueltas — hechas o descartadas: el "qué pasó y por qué". A diferencia de [`./handoff.md`](./handoff.md), **se acumula**: cada tarea resuelta agrega una entrada, sin sobrescribir las anteriores. La cola de pendientes vive en [`./backlog.md`](./backlog.md).

- **Entradas nuevas van arriba** (la más reciente primero). Cada una marca su tipo: ✅ **Hecha** o ❌ **Descartada** (el motivo del descarte queda para que no se vuelva a proponer sin verlo).
- **Formato:** `## <fecha> — ✅|❌ [Tarea N —] <título>` (el segmento `Tarea N —` solo si la tarea tenía número en `backlog.md`; ese número viaja con ella y no se reasigna; las entradas sin número no se numeran retroactivamente). Debajo, 3 a 5 líneas: qué se hizo y **por qué** (el motivo, no la descripción técnica).
- **Qué no va:** lo que ya dice el código, el diff o el commit, ni lo que explica otro archivo (`decisions.md`, `architecture.md`): linkearlo.
- **Cómo leerlo:** no hace falta leerlo entero. Para una tarea puntual, buscar su entrada por número o título; para el contexto reciente, las primeras entradas.

---

## 2026-10-10 — ✅ Tarea 19 — Crear repo hijo usage-meter

- `usage-meter` salió a su propio repo público, `Gersom/claude-mod-usage-meter`, con sus 25 commits de historial (extraídos con `git subtree split`) y el repo vive en `mods/usage-meter/`; el central dejó de versionarlo. El prefijo `claude-mod-` agrupa los repos de la familia y se ve en la lista de GitHub; el nombre del plugin sigue siendo `usage-meter`.
- Se ignoran en el mod `tsconfig.json` y `.claude-plugin/types/` porque Claude Code los genera al cargarlo. Un clon limpio valida y pasa los 63 tests sin ellos; no se probó cargarlo con `--plugin-dir` desde el clon. La regla de commits entre repos está en [`rules.md`](./rules.md).

## 2026-10-10 — ✅ Tarea 18 — Preparar repo central para marketplace

- `claude-mods` pasó a ser el repo central `Gersom/gersom-claude-mods` (renombrado con `gh`): lleva el catálogo (`.claude-plugin/marketplace.json`, hoy sin plugins) y la documentación, y cada mod vive en su propio repo dentro de `mods/`, ignorada por git. Así cada mod se versiona y se actualiza por separado, y desde el central se puede leer y editar todos.
- Para no tocar la Regla 9 (fija) se agregó la regla específica «Cada mod es un repo aparte» en [`rules.md`](./rules.md): el código del mod se commitea en su repo; docs y catálogo, en el central. Validación pasa con el aviso esperado de catálogo vacío. `mods/usage-meter` sigue versionado acá hasta la Tarea 19.

## 2026-10-10 — ✅ Tarea 17 — Título corto «Límite 5h» en la vista de una línea

- En la vista `[=] Una línea` de `usage-meter`, el título en español pasa de `Límite 5 horas` a `Límite 5h`, para ahorrar ancho en una línea que se corta si no cabe. El título completo (`Límite de 5 horas`) y el texto en inglés no cambian. Tests (63/63) pasan.

## 2026-10-10 — ✅ Tarea 11 — Revisar y optimizar el consumo de tokens de usage-meter

- Se revisó el mod y no consume tokens del modelo: el manifiesto no declara skills, agentes, comandos ni MCP, los hooks solo observan (`next(e)` sin modificar) y `breakdown: 'summary'` estima en local, sin llamadas de red. No hizo falta optimizar nada.
- La conclusión sale del código y de los tipos del motor; no se midió en una sesión real. Quedó en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md), sección «Consumo de tokens».

## 2026-10-09 — ✅ Tarea 10 — Multi idioma para usage-meter

- `usage-meter` habla español o inglés según `settings.language`, con diccionarios fijos en el propio mod: ningún agente ni subagente traduce, no hay llamadas a modelos ni consumo de tokens. Si no se detecta el idioma, el panel va en inglés; un botón `[ES]`/`[EN]` lo cambia a mano.
- `settings.language` es texto libre (el del operador es `"Español"`), así que la detección ignora mayúsculas y tildes. El cambio a mano no persiste entre sesiones; no se pidió. Tests (63/63) y validación pasan; revisado a mano por el operador. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-09 — ✅ Tarea 9 — Limpia de código muerto

- Se quitó de `usage-meter` lo que el rediseño de la Tarea 7 dejó sin uso: las barras hechas con texto (`bar()`, `barParts()`, `Row.bar`) y el reparto de celdas de `slicesOf` (`Slice.cells`), que ya no recibe el ancho. Así el código no sugiere un camino de dibujo que ya no existe.
- El panel no cambia. Tests (50/50) y validación pasan. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-09 — ✅ Tarea 7 — Mejorar la UX

- El panel de `usage-meter` se rediseñó a partir de la captura de `/context` y de revisiones del operador en la terminal y la app de escritorio: cabecera con `◆` y porcentaje en recuadro de color, barras a todo el ancho, leyenda de categorías desplegable (`▸ Categorías`), títulos nuevos, botones `Compactar` y `Una línea` al pie y borde gris oscuro solo en la terminal.
- Dos causas de fallos reales en la app: la franja admite `maxRows` y desplaza fuera de vista lo que sobra (los límites desaparecían), y las barras hechas con `█` repetidos se partían; ahora son `Box` con `flexGrow`. Tests (55/55) y validación pasan; revisado a mano por el operador. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-09 — ✅ Tarea 8 — Añadir categorías al contexto

- La fila de Contexto de `usage-meter` muestra debajo una barra segmentada por categoría y una leyenda (nombre, tokens y % de la ventana), para ver qué ocupa el contexto como en `/context`. El desglose sale de `$.session.usage({ breakdown: 'summary' })`, porque `session.measure` no lo trae.
- Se eligió `summary` (estimación local, sin llamadas de red) en lugar de `full`, que cuenta con la API de conteo de tokens (gratuita, pero una llamada por herramienta y archivo de memoria en cada medición). Tests (34/34) y validación pasan; revisado a mano por el operador. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-09 — ✅ Tarea 6 — Añadir tokens al contexto

- La fila de Contexto de `usage-meter` muestra los tokens usados sobre la ventana (`84k de 200k`), en gris atenuado tras el porcentaje, para ver cuánto contexto queda en términos absolutos. `Usage.context` pasa de un número a `{ percent, tokens, window }`.
- El desglose por categorías, que originalmente era parte de esta tarea, pasó a la Tarea 8. Tests (27/27) y validación pasan; no se revisó a mano en sesión. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-08 — ✅ Tarea 5 — Cambiar porcentajes

- Los umbrales de color de `usage-meter` pasan a verde hasta 60 %, amarillo de 61 a 80 % y rojo por encima de 80 %, en lugar de 70 y 90 %. El 80 % exacto quedó en amarillo.
- Tests (23/23) y validación pasan. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-08 — ✅ Tarea 4 — Cambiar diseño del panel

- Se rediseñó el panel de `usage-meter`: contexto en azul y límites en violeta, barra con color de umbral en reposo, animación del porcentaje y la barra al cambiar, y reset en segunda línea en terminales estrechas. Los cálculos no cambiaron.
- Se revisó a mano en sesión (tema oscuro). Los tests no cubren la animación. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md) y [`odd/tasks/cambiar-diseno.md`](../../odd/tasks/cambiar-diseno.md).

## 2026-10-08 — ✅ Tarea 3 — Construir el primer mod

- Se construyó `usage-meter`: un hook que muestra sobre el prompt un recuadro con el % de contexto y de los límites de 5 horas y semanal, con color por umbral y el tiempo de restablecimiento, para ver el consumo de un vistazo.
- Se probó en una sesión real tras habilitar la recarga en caliente; se ajustó la alineación de las barras (columnas de ancho fijo) y el título «Uso» dentro del recuadro. Detalle en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-08 — ✅ Tarea 2 — Definir de qué trata el primer mod

- El primer mod es `usage-meter`: un hook que muestra en un recuadro solo porcentajes de contexto y de los límites de 5 horas y semanal, con su tiempo de restablecimiento, para saber de un vistazo cuánto se va consumiendo sin ver detalles.
- Se verificó que la API de hooks entrega esos datos (`session.measure`) antes de fijar la definición. Diseño y decisiones en [`mods/usage-meter/README.md`](../../mods/usage-meter/README.md).

## 2026-10-08 — ✅ Tarea 1 — Iniciar estructura de carpetas

- Se definió que cada mod vive en `mods/<nombre>/` con un README que explica qué hace, para que la colección escale sin mezclarse con las herramientas del repo (`.claude/`).
- El README de convención va en la raíz del repo (no en `mods/`), porque es la presentación de todo el proyecto. Ver [`architecture.md`](../project/architecture.md).

## 2026-10-08 — ✅ Documentación de contexto inicial

- Se generó `docs/` con agent-context-kit (set completo, etapa idea/setup) para que cualquier agente sepa en qué punto está el proyecto sin depender de una conversación.
