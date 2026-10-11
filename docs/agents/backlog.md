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

**Próximo número de tarea:** 26

---

<!-- agent-context-kit:section=free -->
## Tareas libres

### Tarea 15 — Iniciar nuevo mod claude-radar

- **Descripción:** construir el plugin `claude-radar`, un monitor visual pasivo del agente principal y sus subagentes, según el documento [`docs/claude-radar.md`](../claude-radar.md).
- **Decisiones/temas a definir antes de empezar:** el documento pide, antes de implementar, explicar el plan y esperar autorización (mediana a grande: plan primero, Regla 2); verificar las APIs reales de la versión instalada (eventos de subagentes, tareas) y cargar la skill `plugin-authoring`.
- **Bloqueos:** Ninguno.
- **Desbloquea:** Tarea 16.
- **Agregada:** 2026-10-09

### Tarea 14 — Refinar el mod de caché

- **Descripción:** refinar `cache-watch` (Tarea 13): cambiar su UX y agregarle más información.
- **Decisiones/temas a definir antes de empezar:** qué cambios de UX y qué datos extra; lo define el operador (ideas ya habladas: % de aciertos de la última petición y de la sesión, tokens leídos y escritos de caché).
- **Bloqueos:** [Resuelto el 2026-10-10] — [dependencia] Tarea 13 — el mod de caché aún no existía.
- **Agregada:** 2026-10-09

<!-- agent-context-kit:section=blocked -->
## Tareas bloqueadas / pospuestas

### Tarea 16 — Refinar el mod claude-radar

- **Descripción:** ajustar `claude-radar` (Tarea 15) tras verlo en uso.
- **Decisiones/temas a definir antes de empezar:** qué refinar; lo define el operador al ver el mod.
- **Bloqueos:** [dependencia] Tarea 15 — `claude-radar` aún no existe.
- **Agregada:** 2026-10-09

<!-- agent-context-kit:section=grouped -->
## Tareas agrupadas

No aplica todavía — ningún grupo formado.

### Tarea 25 — Soporte multi-idioma en claude-radar

- **Descripción:** agregar soporte multi-idioma a `claude-radar` (español/inglés) igual que `usage-meter` y `cache-watch`, pero sin botón: el idioma se detecta solo desde `settings.language` y, si no se puede, va en inglés por defecto.
- **Decisiones/temas a definir antes de empezar:** confirmar que el mod destinatario es `claude-radar` (supuesto del agente: `cache-watch` ya detecta el idioma y `usage-meter` también).
- **Bloqueos:** [dependencia] Tarea 15 — `claude-radar` aún no existe.
- **Agregada:** 2026-10-10
