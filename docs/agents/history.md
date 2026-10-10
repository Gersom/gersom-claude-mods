# History

Historial de tareas resueltas — hechas o descartadas: el "qué pasó y por qué". A diferencia de [`./handoff.md`](./handoff.md), **se acumula**: cada tarea resuelta agrega una entrada, sin sobrescribir las anteriores. La cola de pendientes vive en [`./backlog.md`](./backlog.md).

- **Entradas nuevas van arriba** (la más reciente primero). Cada una marca su tipo: ✅ **Hecha** o ❌ **Descartada** (el motivo del descarte queda para que no se vuelva a proponer sin verlo).
- **Formato:** `## <fecha> — ✅|❌ [Tarea N —] <título>` (el segmento `Tarea N —` solo si la tarea tenía número en `backlog.md`; ese número viaja con ella y no se reasigna; las entradas sin número no se numeran retroactivamente). Debajo, 3 a 5 líneas: qué se hizo y **por qué** (el motivo, no la descripción técnica).
- **Qué no va:** lo que ya dice el código, el diff o el commit, ni lo que explica otro archivo (`decisions.md`, `architecture.md`): linkearlo.
- **Cómo leerlo:** no hace falta leerlo entero. Para una tarea puntual, buscar su entrada por número o título; para el contexto reciente, las primeras entradas.

---

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
