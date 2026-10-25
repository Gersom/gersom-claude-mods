# Backlog

Cola de tareas pendientes: el "qué falta" a nivel proyecto. No es la tarea en curso (eso vive en [`./handoff.md`](./handoff.md)) ni lo ya cerrado ([`./history.md`](./history.md)).

**Ciclo de vida:** una tarea se agrega acá al identificarla; al empezar a trabajarla se saca de esta lista y pasa a `handoff.md`; al cerrarla (hecha o descartada) se registra en `history.md`. No dejar acá tareas en curso o cerradas.

**Dos secciones:** "Tareas libres" (listas para tomar) y "Tareas bloqueadas / pospuestas". Cuando el motivo de un bloqueo deja de aplicar, la tarea pasa a libres (Regla 7 de `rules.md`; `Bloqueos` no se borra, se marca como resuelto).

**Numeración:** cada tarea tiene un número correlativo fijo, asignado al crearla y **nunca reutilizado**, ni siquiera al cerrarla: sirve para referenciarla sin ambigüedad ("la tarea 3") y viaja a su entrada de `history.md`. No es un orden de cola. Para agregar una tarea: usar "Próximo número de tarea" (más abajo) y dejarlo en N+1; también se numeran las tareas nuevas que surjan de una tarea en curso.

**Formato de cada tarea** (`### Tarea N — título`), todo breve — `Detalles` solo si hace falta, y si el detalle ya vive en otro archivo (`decisions.md`, `known-issues.md`), enlazarlo:
- **Descripción:** de qué trata (1–3 líneas).
- **Decisiones/temas a definir antes de empezar:** qué resolver o preguntarle al operador antes de arrancar; "Ninguno" si está todo definido.
- **Bloqueos:** "Ninguno", o un valor que **empieza** con `[dependencia]` (no se puede empezar técnicamente) o `[postergada]` (conviene esperar) y el motivo. Con bloqueo va en "bloqueadas / pospuestas"; si no, en "libres". Si una tarea ya desbloqueada (`[Resuelto el <fecha>] — …`) se vuelve a bloquear, el bloqueo vigente va **primero** y el historial resuelto después, porque el script de seguimiento toma el tag con el que empieza el campo.
- **Desbloquea:** (opcional) qué tareas quedan libres al cerrar esta.
- **Disparador:** cuándo corresponde tomarla; por defecto "cuando el operador pregunte por tareas pendientes".
- **Detalles:** contexto extendido, solo si hace falta.
- **Agregada:** fecha.

**Agrupamiento (solo en "Tareas libres"):** si superan las 15 tareas (Regla 7), se evalúa agrupar 2 o más que compartan un objetivo real — el grupo entero tiene que caber en una frase de objetivo compartido, sin forzar con "y". El grupo aparece en libres como un bloque `### Grupo — título (Tareas N, M)` con un `Resumen` de una frase; el detalle de cada tarea (`#### Tarea N — título`, mismo formato) se mueve a "Tareas agrupadas", que no hace falta leer salvo para tomar una. Un grupo que queda con una sola tarea se desarma.

**Anclas de sección:** no borres ni muevas los comentarios `<!-- agent-context-kit:section=... -->` (`free`, `blocked`, `grouped`) que preceden a cada sección: los usa el script de seguimiento de tareas de agent-context-kit.

**Próximo número de tarea:** 36

---

<!-- agent-context-kit:section=free -->
## Tareas libres

### Tarea 32 — Mejoras de UX en agent-radar

- **Descripción:** ponerle borde y espacio a la banda de `agent-radar` como en `cache-watch` (borde redondo gris `#4b5563`, fila en blanco entre paneles en el escritorio) y cambiar el botón `[ ● Claude Radar: ON ]` a solo `ON`/`OFF`.
- **Decisiones/temas a definir antes de empezar:** ninguno; el nombre «Claude Radar» ya está a la izquierda de la banda. Conviene hacerla junto con las Tareas 30 o 31 si tocan la misma banda.
- **Bloqueos:** Ninguno.
- **Agregada:** 2026-10-11

### Tarea 31 — Persistencia del estado de agent-radar

- **Descripción:** persistir en `$.store` el estado de `agent-radar`: mod quitado de la barra del prompt, pane abierto y mod ON/OFF (hoy solo se guarda ON/OFF).
- **Decisiones/temas a definir antes de empezar:** reabrir el pane al empezar la sesión choca con la regla de que el mod no abre el pane por su cuenta (bajo 144 columnas no se coloca si no lo pide el usuario): decidir si se reabre solo si cabe, o si basta recordar la preferencia. El estado «quitado de la barra» ya se persiste (Tarea 30, clave `bandHidden`); falta el del pane.
- **Bloqueos:** [Resuelto el 2026-10-11] — [dependencia] Tarea 30: el estado «mod quitado de la barra» no existía (ya existe, clave `bandHidden`; falta persistir el pane abierto).
- **Agregada:** 2026-10-11

### Tarea 35 — Agregar detalles faltantes en agent-radar (modelo y esfuerzo)

- **Descripción:** mostrar en el pane de `agent-radar`, además del nombre, el modelo que usa el agente líder y cada subagente, y su esfuerzo.
- **Decisiones/temas a definir antes de empezar:** verificar qué datos da el motor: `agent.spawn` devuelve `model` del subagente (alias o id), pero no está comprobado de dónde sale el modelo del agente líder ni si existe un dato de esfuerzo para ninguno de los dos (mirar `.claude-plugin/types/claude-code/index.d.ts` y `$.settings.read()`); si no existe, decidir si se omite o se infiere. Decidir también el formato (en la misma línea del nombre o debajo) y cómo se acorta el id del modelo en un pane angosto.
- **Bloqueos:** Ninguno.
- **Agregada:** 2026-10-25

<!-- agent-context-kit:section=blocked -->
## Tareas bloqueadas / pospuestas

<!-- agent-context-kit:section=grouped -->
## Tareas agrupadas

No aplica todavía — ningún grupo formado.
