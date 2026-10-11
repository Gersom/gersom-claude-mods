# Claude Radar — Monitor visual de Claude Code y sus subagentes

Antes de comenzar, lee completamente estas instrucciones. Explica qué implementarás, qué archivos crearás o modificarás, qué comandos ejecutarás y cualquier costo o cambio difícil de revertir. Solicita mi autorización y espera mi confirmación antes de comenzar.

Construye un plugin llamado **Claude Radar**, cuyo identificador será `claude-radar`.

Claude Radar es un monitor visual para Claude Code que permite observar en tiempo real el trabajo del agente principal y sus subagentes, incluidos los agentes personalizados.

Su propósito es ofrecer un resumen visual limpio, sencillo y comprensible, ocultando temporalmente la información técnica durante la ejecución, sin modificar el comportamiento de Claude Code.

**Principios fundamentales:**

- Funcionamiento completamente pasivo.
- Mínimo consumo adicional de tokens.
- Ninguna llamada adicional a modelos de IA.
- Ninguna interferencia con el agente principal ni sus subagentes.
- Conservación completa de las respuestas y reportes finales.
- Actualización visual automática mediante eventos y metadatos existentes.

Antes de implementar, carga la skill `plugin-authoring` y sigue sus instrucciones.

Utiliza function hooks y recarga en caliente si la API disponible lo permite. No utilices shell-script hooks ni servidores MCP.

Verifica las APIs reales disponibles en la versión instalada de Claude Code antes de implementar funcionalidades.

## 1. Interfaz visual

Mostrar una sección justo encima del campo de entrada de Claude Code.

Ejemplo:

```text
Build my landing page · 2m 35s         [ ● Claude Radar: ON ]

✓ Analyze project structure     ██████████  Done
▶ Implement authentication      ████░░░░░░  Working
○ Run final tests               ░░░░░░░░░░  Next

Subagents                              2 active

● frontend-developer                        1m 20s
  Building login components                 Working

● backend-developer                            45s
  Reviewing authentication routes           Working
```

### Encabezado

- Título corto de la actividad principal.
- Tiempo transcurrido desde el inicio.
- Botón `Claude Radar: ON/OFF` alineado a la derecha.
- El botón debe permanecer visible incluso cuando Claude esté inactivo.
- Adaptar el contenido al ancho disponible.

### Checklist principal

- Completadas: ✓ verde, nombre atenuado, barra completa y `Done`.
- Actual: ▶, nombre destacado y barra de progreso.
- Pendientes: ○, nombres atenuados y `Next` o `Up next`.
- Barras de 10 segmentos.
- Si no existe un porcentaje real, utilizar una animación indeterminada con el texto `Working`.
- Nunca inventar porcentajes.

El checklist solo debe utilizar información real que Claude Code ya proporcione.

## 2. Estados del agente principal

Detectar y mostrar:

- `Working`: actividad y tiempo transcurrido.
- `Needs you`: Claude requiere una respuesta o autorización.
- `Stuck`: existe un problema identificado.
- `Stopped`: ejecución interrumpida.
- `Done`: trabajo finalizado.

Al finalizar, mostrar `All done` y la duración total.

Después de 5 segundos, contraer la interfaz a una sola línea.

Conservar todos los controles originales de permisos, preguntas y confirmaciones.

No ocultar errores importantes ni impedir que el usuario consulte sus detalles originales.

## 3. Detección automática de tareas

Claude Radar debe observar pasivamente el trabajo existente.

**No obligar a Claude a generar planes ni reportar avances.**

Utilizar, cuando estén disponibles:

- `TodoWrite`
- `TaskCreate`
- `TaskUpdate`
- Eventos de inicio y finalización de turnos.
- Eventos de ejecución de herramientas.
- Permisos, errores y cancelaciones.

Si Claude utiliza tareas, representarlas automáticamente.

Si no existen tareas:

- Mostrar `Working on your request`.
- Utilizar progreso indeterminado.
- No inventar pasos.
- No generar listas artificiales.
- No solicitar explicaciones al modelo.
- No bloquear herramientas.
- No modificar el flujo de trabajo.

Obtener el título mediante lógica local usando información ya disponible.

## 4. Monitoreo de subagentes

Añadir una sección `Subagents` debajo del checklist principal.

Debe mostrar automáticamente qué subagentes están activos, sus nombres, actividades y estados.

### 4.1. Detección

Detectar tanto agentes nativos como personalizados.

Incluir los definidos en:

- `~/.claude/agents/`
- `.claude/agents/` del proyecto.
- Agentes proporcionados por plugins.
- Otros agentes compatibles con Claude Code.

Utilizar `SubagentStart`, `SubagentStop` o los eventos equivalentes disponibles.

Identificar cada ejecución mediante `agent_id`.

Evitar confundir instancias distintas del mismo agente.

Asociar los eventos con la sesión correspondiente cuando existan identificadores de sesión.

### 4.2. Nombres personalizados

Mostrar el nombre real del agente, priorizando `agent_type` cuando corresponda al nombre de su definición.

Ejemplos:

- `frontend-developer`
- `backend-developer`
- `database-specialist`
- `code-reviewer`
- `Explore`
- `Plan`

No reemplazar nombres personalizados por etiquetas genéricas.

No modificar las definiciones de agentes.

No leer archivos de configuración repetidamente si los metadatos existentes ya permiten identificar al agente.

### 4.3. Actividad de cada subagente

Mostrar debajo de su nombre una descripción breve de lo que está haciendo.

Ejemplo:

```text
● frontend-developer                      1m 20s
  Building login components               Working
```

Obtener esa información únicamente de:

- Descripción original de la tarea delegada.
- Metadatos de ejecución.
- Eventos atribuibles al subagente.
- Información proporcionada directamente por la API.

Cuando existan eventos de herramientas vinculados a un `agent_id`, actualizar la actividad correspondiente.

Utilizar descripciones locales y sencillas:

- Lectura de archivos → `Reading project files`.
- Modificación de archivos → `Updating project files`.
- Ejecución de pruebas → `Running tests`.
- Búsquedas → `Searching project information`.

No mostrar rutas completas, comandos ni código en las descripciones principales.

No inventar actividades.

Si no existe información suficiente, mostrar la tarea delegada o simplemente `Working`.

No realizar llamadas a modelos para generar descripciones.

### 4.4. Subagentes simultáneos

Admitir múltiples ejecuciones paralelas.

Requisitos:

- Estado independiente por instancia.
- Identificación mediante `agent_id`.
- Soporte para varios agentes con el mismo nombre.
- Contador de subagentes activos.
- Actualizaciones independientes.
- Compatibilidad con ejecuciones en segundo plano cuando sus eventos sean accesibles.
- No confundir la finalización de un subagente con la del agente principal.

Si existen subagentes anidados, mostrar su jerarquía únicamente cuando los metadatos permitan identificarla con fiabilidad.

### 4.5. Estados

Representar, cuando exista evidencia suficiente:

- `Working`: ejecutándose.
- `Needs you`: requiere intervención.
- `Done`: finalización exitosa confirmada.
- `Failed`: error confirmado.
- `Stopped`: interrupción confirmada.

Mostrar tiempo de ejecución individual.

Al finalizar:

- Detener su contador.
- Actualizar su estado.
- Mantenerlo visible brevemente.
- Retirarlo después de un intervalo corto de la sección de actividad.

No asumir que un evento de finalización significa éxito si la API no proporciona esa información.

Si no hay subagentes, ocultar la sección.

## 5. Optimización estricta de tokens

**Claude Radar debe funcionar exclusivamente como observador pasivo.**

Requisitos obligatorios:

- No realizar llamadas adicionales a Haiku ni a ningún otro modelo.
- No utilizar hooks `prompt` o `agent` que invoquen modelos.
- No utilizar `prompt.compose`.
- No inyectar instrucciones en el contexto.
- No crear subagentes de supervisión.
- No registrar herramientas de progreso como `plan_steps` o `report_progress`.
- No obligar a crear planes.
- No exigir reportes de progreso.
- No bloquear herramientas para forzar comportamientos.
- No agregar mensajes artificiales al historial.
- No solicitar resúmenes intermedios.
- No enviar eventos de progreso a modelos.
- No utilizar IA para generar títulos, porcentajes o actividades.
- No reprocesar conversaciones completas mediante IA.
- No enviar diffs, archivos o salidas de comandos a modelos adicionales.
- No cargar instrucciones del plugin en el contexto durante su funcionamiento normal.
- No modificar las instrucciones ni estrategias del agente principal o sus subagentes.

Toda la lógica debe ejecutarse localmente con TypeScript.

Actualizar el estado incrementalmente utilizando los eventos disponibles.

No realizar lecturas recurrentes de transcripciones de subagentes para simular seguimiento en tiempo real.

Evitar almacenar contenido extenso o innecesario.

El objetivo es que Claude Radar no provoque consumo adicional de tokens durante su funcionamiento normal, siempre que las APIs disponibles permitan una implementación completamente local.

## 6. Ocultar información técnica

Cuando Claude Radar esté activado, ocultar visualmente durante la ejecución:

- `ToolUse`
- `ToolResult`
- `ToolGroup`
- Indicadores técnicos de `ToolProgress`
- Diferencias entre archivos.
- Salidas de comandos.

Aplicar estas reglas a la actividad del agente principal y sus subagentes cuando corresponda.

La ocultación debe ser exclusivamente visual.

No bloquear, modificar, cancelar ni alterar las herramientas.

No eliminar información del historial original.

Cuando Claude Radar esté desactivado, restaurar la interfaz normal.

### Protección absoluta de respuestas finales

**Claude Radar nunca debe modificar, ocultar, resumir ni sustituir la respuesta final de Claude Code.**

Conservar:

- Reportes de archivos creados, modificados o eliminados.
- Descripciones de cambios.
- Resultados de pruebas.
- Advertencias.
- Errores.
- Recomendaciones.
- Cualquier otro contenido final.

No generar un reporte alternativo que sustituya al original.

El indicador visual `All done` puede coexistir con la respuesta final, pero nunca reemplazarla.

Esta regla tiene prioridad sobre todas las demás funcionalidades.

## 7. Botón ON/OFF

El plugin debe controlarse exclusivamente mediante un botón.

- `ON`: mostrar Claude Radar y ocultar las filas técnicas durante el trabajo.
- `OFF`: restaurar la interfaz habitual de Claude Code.
- Mostrar una notificación visual breve al cambiar.
- Guardar la configuración mediante almacenamiento persistente, como `$.store`, cuando esté disponible.
- Recordar la preferencia después de reiniciar.
- Estado inicial: `ON`.

El botón controla tanto el checklist principal como la sección de subagentes.

**No crear `/simple`, `/radar` ni ningún otro slash command.**

El botón debe funcionar en las superficies compatibles, utilizando únicamente APIs disponibles.

## 8. Formato y animaciones

### Nombres de actividades

Aplicar una función normalizadora:

- Eliminar rutas de archivos y fragmentos de código.
- Colapsar espacios.
- Capitalizar la primera letra.
- Limitar a 40 caracteres.
- Recortar por palabras.
- Usar `Working on it` si no existe contenido válido.

Preservar los nombres reales de los subagentes, aplicando únicamente truncamiento visual cuando sea necesario.

Nunca modificar el contenido original de las respuestas de Claude.

### Animaciones

- Actualizar animaciones cada 250 ms cuando sea necesario.
- Detener los temporizadores durante la inactividad.
- Utilizar animaciones independientes visualmente para agentes activos.
- Compartir un único temporizador local siempre que sea posible.
- Evitar renderizados innecesarios.
- No realizar llamadas al modelo para animaciones.

### Compatibilidad

- Adaptar la interfaz a terminales estrechas.
- Evitar que las filas se desborden.
- No interferir con encuestas ni controles especiales.
- Priorizar la visualización de agentes activos cuando haya poco espacio.
- Utilizar representaciones simplificadas si alguna API no permite la versión completa.

## 9. Arquitectura

Organizar el código modularmente.

Estructura preferida:

- `register.tsx`: entrada y registro del plugin.
- `claude-radar.tsx`: lógica, estado y representación visual.
- `types/index.d.ts`: tipos compartidos.

Identificador del plugin: `claude-radar`.

Clave de estado: `claudeRadarState`.

Tipos sugeridos:

```typescript
type AgentPhase =
  | "working"
  | "needsYou"
  | "stuck"
  | "stopped"
  | "done";

type SubagentStatus =
  | "working"
  | "needsYou"
  | "done"
  | "failed"
  | "stopped";

type SubagentState = {
  id: string;
  sessionId: string;
  name: string;
  task: string | null;
  activity: string | null;
  status: SubagentStatus;
  startedAt: number;
  finishedAt: number | null;
};

type ClaudeRadarState = {
  claudeRadarEnabled: boolean;
  checklist: {
    title: string;
    phase: AgentPhase;
    tasks: Array<{
      id: string;
      name: string;
      status: "done" | "active" | "upcoming";
      percent: number | null;
      hasReported: boolean;
    }>;
    needsYouReason: string | null;
    stuckReason: string | null;
    startedAt: number | null;
    finishedAt: number | null;
    isCollapsed: boolean;
  };
  subagents: Record<string, SubagentState>;
  tick: number;
};
```

Utilizar únicamente APIs documentadas y disponibles en la versión instalada de Claude Code.

No inventar métodos, propiedades ni eventos.

Si alguna funcionalidad no está soportada, explicar la limitación y utilizar una alternativa compatible.

No modificar archivos de agentes personalizados, configuraciones globales ni otros plugins sin autorización.

Si ya existe una instalación anterior de Clean View, no eliminarla ni migrar sus datos automáticamente sin autorización explícita.

## 10. Pruebas

Utilizar el sistema oficial de pruebas disponible. Ejecutar `claude plugin test` si corresponde.

Verificar:

1. El botón `Claude Radar: ON/OFF` funciona.
2. La configuración persiste después de reiniciar.
3. No existen comandos `/simple` ni `/radar`.
4. Claude no necesita crear planes para trabajar.
5. No se registran herramientas adicionales de progreso.
6. No se realizan llamadas adicionales a modelos.
7. No se inyectan instrucciones al contexto.
8. Las tareas existentes aparecen automáticamente.
9. Cuando no existen tareas, se muestra progreso indeterminado.
10. Las solicitudes de permisos siguen funcionando.
11. Las filas técnicas se ocultan únicamente de forma visual.
12. Las respuestas finales y reportes de archivos permanecen intactos.
13. Los agentes personalizados muestran sus nombres reales.
14. Se detecta el inicio de cada subagente.
15. Se detecta la finalización de cada subagente.
16. Varias instancias del mismo agente permanecen independientes.
17. Los subagentes paralelos muestran estados separados.
18. Las actividades se actualizan con datos verificables.
19. Los agentes sin información de actividad muestran `Working`.
20. Los subagentes terminados dejan de aparecer como activos.
21. La sección de subagentes desaparece cuando está vacía.
22. No se crean subagentes de supervisión.
23. No se reprocesan conversaciones completas mediante IA.
24. Las animaciones se detienen durante la inactividad.
25. La interfaz funciona en las superficies compatibles.

## 11. Criterios de finalización

Claude Radar estará terminado cuando:

- Se active y desactive únicamente mediante su botón.
- Muestre el progreso observable del agente principal.
- Oculte visualmente la información técnica durante el trabajo.
- Detecte automáticamente subagentes nativos y personalizados.
- Muestre nombres, actividades observables y estados individuales.
- Soporte subagentes paralelos.
- No genere llamadas adicionales a modelos.
- No obligue a crear planes ni reportes.
- No modifique el funcionamiento de Claude Code.
- Conserve las respuestas finales completamente intactas.
- Mantenga la configuración entre sesiones.
- Supere las pruebas disponibles.

Al finalizar, explica brevemente cómo instalar Claude Radar, cómo activar y desactivar el botón y cómo trasladar el plugin a otra computadora. Indica cualquier limitación real de las APIs para observar subagentes.

**Prioridad principal: consumo adicional de tokens mínimo, funcionamiento nativo intacto, monitoreo fiable de subagentes e interfaz visual limpia.**