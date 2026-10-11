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

**Próximo número de tarea:** 35

---

<!-- agent-context-kit:section=free -->
## Tareas libres

### Tarea 32 — Mejoras de UX en agent-radar

- **Descripción:** ponerle borde y espacio a la banda de `agent-radar` como en `cache-watch` (borde redondo gris `#4b5563`, fila en blanco entre paneles en el escritorio) y cambiar el botón `[ ● Claude Radar: ON ]` a solo `ON`/`OFF`.
- **Decisiones/temas a definir antes de empezar:** ninguno; el nombre «Claude Radar» ya está a la izquierda de la banda. Conviene hacerla junto con las Tareas 30 o 31 si tocan la misma banda.
- **Bloqueos:** Ninguno.
- **Agregada:** 2026-10-11

### Tarea 34 — Revisar el error de subagentes en agent-radar

- **Descripción:** los subagentes no se muestran en `agent-radar` cuando se ejecutan (ni en el pane ni en la lista viva); revisar por qué.
- **Decisiones/temas a definir antes de empezar:** reproducir primero: superficie (terminal o escritorio), con el pane abierto antes o después de lanzar el subagente, y si aparece al terminar en el historial. Hipótesis a comprobar, sin darlas por ciertas: que `agent.spawn` no llegue al plugin con `agentId` en `next(e)` para los subagentes del tool `Agent` (el resultado quizá no trae `agentId` o el spawn va por otra ruta); que `turn.complete`/`tool.call` con `agentId` lleguen con otro identificador que el del spawn; que el pane no se redibuje al cambiar `subagents`; que el filtro `origin.plugin === 'engine'` o la poda de terminados los quite. Los tests usan un kit simulado que podría no reflejar el motor real.
- **Bloqueos:** Ninguno.
- **Agregada:** 2026-10-11

### Tarea 31 — Persistencia del estado de agent-radar

- **Descripción:** persistir en `$.store` el estado de `agent-radar`: mod quitado de la barra del prompt, pane abierto y mod ON/OFF (hoy solo se guarda ON/OFF).
- **Decisiones/temas a definir antes de empezar:** reabrir el pane al empezar la sesión choca con la regla de que el mod no abre el pane por su cuenta (bajo 144 columnas no se coloca si no lo pide el usuario): decidir si se reabre solo si cabe, o si basta recordar la preferencia. El estado «quitado de la barra» ya se persiste (Tarea 30, clave `bandHidden`); falta el del pane.
- **Bloqueos:** [Resuelto el 2026-10-11] — [dependencia] Tarea 30: el estado «mod quitado de la barra» no existía (ya existe, clave `bandHidden`; falta persistir el pane abierto).
- **Agregada:** 2026-10-11

<!-- agent-context-kit:section=blocked -->
## Tareas bloqueadas / pospuestas

<!-- agent-context-kit:section=grouped -->
## Tareas agrupadas

No aplica todavía — ningún grupo formado.
