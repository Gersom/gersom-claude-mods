# History

Historial de tareas resueltas — hechas o descartadas: el "qué pasó y por qué". A diferencia de [`./handoff.md`](./handoff.md), **se acumula**: cada tarea resuelta agrega una entrada, sin sobrescribir las anteriores. La cola de pendientes vive en [`./backlog.md`](./backlog.md).

- **Entradas nuevas van arriba** (la más reciente primero). Cada una marca su tipo: ✅ **Hecha** o ❌ **Descartada** (el motivo del descarte queda para que no se vuelva a proponer sin verlo).
- **Formato:** `## <fecha> — ✅|❌ [Tarea N —] <título>` (el segmento `Tarea N —` solo si la tarea tenía número en `backlog.md`; ese número viaja con ella y no se reasigna; las entradas sin número no se numeran retroactivamente). Debajo, 3 a 5 líneas: qué se hizo y **por qué** (el motivo, no la descripción técnica).
- **Qué no va:** lo que ya dice el código, el diff o el commit, ni lo que explica otro archivo (`decisions/`, `architecture.md`): linkearlo.
- **Cómo leerlo:** no hace falta leerlo entero. Para una tarea puntual, buscar su entrada por número o título; para el contexto reciente, las primeras entradas.

---

## 2026-10-27 — ✅ Tarea 43 — Pulir usage-meter: tests del panel y tipos

- `bunx tsc --noEmit` ya no da errores en `usage-meter` (claves de lista como texto y valores posiblemente `undefined` en `format.ts` y sus tests), sin cambiar el comportamiento. Era lo único que quedaba de los pendientes del revisor de la Tarea 40, tras descartar reiniciar el idioma al terminar la sesión, cancelar los timers de la animación y actualizar la descripción del comando.
- No se hicieron los tests del cierre del panel por la persona ni del orden «`ui.open` primer `await`» en el botón: el arnés de pruebas del motor no tiene `$.ui.close` ni deja observar ese orden. Queda anotado en «Limitaciones conocidas» del README del mod; el test del comando cubre el orden de ese camino. 68 tests pasan; sin push.

## 2026-10-27 — ❌ Tarea 41 — Evaluar la UX de usage-meter

- Descartada: al operador le gusta cómo quedó `usage-meter` tras la Tarea 40 (banda de una línea y panel lateral), así que no hay una evaluación que hacer. No se cambió código.
- Si hace falta pulir `usage-meter`, los pendientes menores ya están en la Tarea 43. La Tarea 42 (integración visual de los mods) quedó libre.

## 2026-10-27 — ✅ Tarea 32 — Mejoras de UX en agent-radar

- El botón de `agent-radar` pasa de `[ ● Agent Radar: ON ]` a `[ ● ON ]` / `[ ● OFF ]`: el nombre ya está a la izquierda de la banda y repetirlo ocupaba espacio. Los avisos breves al pulsar conservan `Agent Radar: ON/OFF`.
- Lo del borde y el espacio de la banda (como `cache-watch`) se descartó: el operador está conforme con la banda sin borde, igual que ahora `usage-meter`. No volver a proponerlo sin verlo; la consistencia visual entre mods se evalúa en la Tarea 42. 148 tests pasan y 3 fallan, los mismos de antes (kit 2.1.310). Sin push.

## 2026-10-27 — ✅ Tarea 44 — Renombrar «Claude Radar» a «Agent Radar» en la pantalla

- El título visible de `agent-radar` pasa a «Agent Radar»: banda, botón `Agent Radar: ON/OFF`, avisos, descripción del comando, tests y README del mod. Así coincide con el identificador del plugin (`agent-radar`) en vez de usar un nombre que el kit no permite como id.
- No se tocaron `hooks/claude-radar.tsx`, `docs/claude-radar.md` ni las entradas anteriores de este historial. 148 tests pasan y 3 fallan, los mismos que ya fallaban antes (kit 2.1.310). Sin push.

## 2026-10-27 — ❌ Tarea 31 — Persistencia del estado de agent-radar

- Descartada: ya se guardaban el ON/OFF y «banda quitada»; solo faltaba persistir el panel abierto, y reabrirlo al empezar la sesión choca con la regla de que el mod nunca abre el panel por su cuenta (bajo 144 columnas ni se coloca). Basta con el botón de detalle o `/agent-radar` cuando se necesite.
- No hubo cambios de código. Si se vuelve a proponer, recordar la preferencia sin reabrir solo tampoco aporta lo suficiente.

## 2026-10-27 — ✅ Tarea 40 — Mover usage-meter a un panel lateral

- `usage-meter` pasa a una banda de una línea sobre el prompt, sin borde (`Usage Meter: Contexto 9% · Límite 5h 4% · Semanal 3%` con los botones `[ ◧ Abrir ]` e idioma) y un panel lateral con el detalle: barras, subtítulos bajo la barra, leyenda de categorías siempre abierta. Antes el recuadro con tres vistas ocupaba mucho espacio sobre el prompt, y el panel tiene lugar de sobra. Se eliminaron las vistas compacta y una línea, y el panel nunca se abre solo (botón o `/usage-meter`), igual que `agent-radar`.
- Un revisor no halló bugs funcionales; sus pendientes menores pasaron a la Tarea 43. El operador probó el resultado a mano y funciona; 68 tests y `claude plugin validate .` pasan. Los commits están en el repo del mod (`dd763ea` … `faa5aa9`), sin push.

## 2026-10-26 — ✅ Tarea 39 — Mejoras UX: misma estructura vertical para ejecución actual e historial

- Cada agente del pane de `agent-radar` se dibuja en líneas verticales, igual en «Ejecución actual» y en «Historial»: nombre con `· modelo · esfuerzo`, la tarea, y una línea de estado `Trabajando · tiempo · tokens` con la barra de carga al final. Antes todo iba en una sola línea con columnas a la derecha y el ancho del pane no daba para tanto.
- Hay una sola barra por el agente principal y una por cada subagente activo, sin porcentajes y sin barras en el checklist, en agentes terminados ni en el historial. Se quitaron las columnas, los umbrales de ancho y los separadores entre agentes. El historial no usa el verde (lo terminado con éxito va en el color normal). Un revisor halló que los títulos y el modelo no se encogían y podían desbordar en panes estrechos; se corrigió. Sin probar en un Claude Code real; 148 tests pasan y 3 fallan por un cambio del kit (2.1.310) anterior a esta tarea.

## 2026-10-26 — ✅ Tarea 38 — Mejoras UX: títulos de sección de agent-radar

- Los títulos del pane de `agent-radar` («Ejecución actual» e «Historial») tienen el mismo formato, `<título> · <subtítulos>`, con los subtítulos en gris (el tiempo y los tokens del turno, o el número de ejecuciones), y debajo una línea de guiones bajos de 30 columnas, igual en las dos secciones, desde el inicio de la fila y con una fila en blanco después. Antes el tiempo total iba alineado a la derecha y la línea entre secciones se veía muy llamativa.
- Se descartó la palabra «Tiempo total» del título (y su texto) y los paréntesis del contador. Sin probar en un Claude Code real; 146 tests pasan y 3 fallan: ya fallaban antes de esta tarea (desde que el Claude Code instalado es el 2.1.310, el mod se hizo con el 2.1.296) y no se investigaron.

## 2026-10-26 — ✅ Tarea 37 — Más mejoras UX en agent-radar

- El pane de `agent-radar` adopta el diseño de referencia del operador, adaptado a lo que se dibuja en terminal y escritorio: tokens por agente y por turno, encabezado con tiempo total y tokens, contador de subagentes activos, filas alineadas con barra sin porcentaje y separadores entre secciones. El historial va siempre abierto, sin plegables, y sus turnos se separan solo con una fila en blanco porque las líneas resultaban invasivas.
- Los tokens salen del `usage` que el motor ya informa en cada `turn.step` (entrada + salida + caché escrita, sin lecturas de caché), así que no cuestan tokens al modelo. Las barras siguen sin inventar porcentajes. El título del turno admite 80 caracteres. Sin probar en un Claude Code real; 148 tests. Pendiente menor: los umbrales de ancho no descuentan la sangría (nombre muy corto en panes de ~38 columnas).

## 2026-10-26 — ✅ Tarea 36 — Mejoras UX en el pane de agent-radar (ejecución actual e historial por turno)

- El pane de `agent-radar` se agrupa por turno: «Ejecución actual» (título, barra de estado, Main agent / Agente principal con modelo, esfuerzo, tiempo y checklist, y subagentes con su tarea) e «Historial» con un grupo por turno terminado (hasta 10, solo en memoria). Sin turno en marcha dice que todo está listo. Antes el historial era una lista plana de subagentes y no se veía qué subagente era de qué petición.
- Un turno dura hasta que terminan el principal y todos sus subagentes; cancelar lo archiva de inmediato y detiene a los subagentes activos. El revisor halló que `turn.start` también llega por subagentes y partía el turno; ahora se ignora. Sin probar en un Claude Code real; 137 tests. Pendiente menor: el historial no guarda el motivo de un error.

## 2026-10-25 — ✅ Tarea 35 — Agregar detalles faltantes en agent-radar (modelo y esfuerzo)

- El pane de `agent-radar` muestra el modelo y el esfuerzo del agente principal (en `Now`) y de cada subagente (junto al nombre), en forma corta (`opus-4-5 · high`). Antes solo salía el nombre y no se sabía con qué modelo trabajaba cada agente.
- Salen del hook `turn.step`, que el motor lanza en cada petición al modelo con `model` y `effort` (este falta en modelos sin esfuerzo); solo observa, no cuesta tokens. Un subagente arranca con el modelo de su spawn hasta su primera petición. 128 tests; sin probar en un Claude Code real.

## 2026-10-11 — ❌ Tarea 34 — Revisar el error de subagentes en agent-radar

- Descartada: no era un fallo de código. Los subagentes no aparecían en el pane porque el mod en uso era una versión anterior sin recargar; tras recargarlo (y con un diagnóstico temporal que ya se quitó) aparecieron bien en el pane.
- Si vuelve a pasar, recargar el mod antes de investigar. No hubo cambios de código.

## 2026-10-11 — ✅ Tarea 30 — Comando y botón para quitar agent-radar de la barra del prompt

- `agent-radar` ganó el botón `[ ✕ Hide ]` y los comandos `/agent-radar hide` y `/agent-radar show`: quitan y devuelven la banda sin apagar el radar (el pane y el ocultar filas técnicas siguen según ON/OFF). Se vuelve a mostrar solo con el comando, no con una línea mínima, para que «quitar» sea de verdad quitar.
- La elección se guarda en `$.store` (`bandHidden`) y sobrevive a las sesiones, lo que deja listo el estado que necesita la Tarea 31. 122 tests; sin probar en un Claude Code real.

## 2026-10-11 — ✅ Tarea 29 — Comando para abrir el pane de agent-radar

- `agent-radar` registra `/agent-radar`: sin argumento alterna el pane de detalle, y `open`/`close` lo abren o cierran a la fuerza; con el radar en OFF avisa y no abre nada. Es una segunda vía además del botón de la banda. El documento original del mod prohibía comandos slash; el operador lo pidió expresamente, así que el README lo aclara y el test pasó a exigir que solo exista este.
- Para que el motor lo trate como una petición del usuario, `$.ui.open` tiene que ser el primer `await` del manejador (lo mismo que arregló el botón en terminal), por eso decide con variables de módulo y no lee estado antes de abrir. Su respuesta de una línea queda en la conversación, así que el consumo del mod pasó de «cero» a «prácticamente cero». Probado a mano por el operador; 118 tests.

## 2026-10-11 — ✅ Tarea 33 — Crear el repo remoto de agent-radar

- Se creó `Gersom/claude-mod-agent-radar` (público, igual que los otros mods), se subió `mods/agent-radar` con sus 10 commits y se añadió al catálogo del central (`marketplace.json` y la tabla de mods del README). Hasta ahora el trabajo de `agent-radar` vivía solo en el disco local.
- Público porque el catálogo instala los mods desde GitHub sin credenciales. No se comprobó la instalación desde el catálogo en una sesión real.

## 2026-10-11 — ✅ Tarea 25 — Soporte multi-idioma en agent-radar

- `agent-radar` habla español o inglés según `settings.language`, sin botón de idioma, y cae a inglés cuando no puede detectarlo; «Claude Radar» no se traduce. Era lo que ya hacían `cache-watch` y `usage-meter`, con la diferencia de que aquí el idioma no se elige a mano.
- Para que el idioma pueda cambiar entre sesiones, el estado dejó de guardar frases ya escritas y guarda códigos (razones, actividades, título por defecto) que el dibujo traduce con el diccionario. Probado a mano por el operador; 108 tests.

## 2026-10-11 — ✅ Tarea 16 — Refinar el mod agent-radar

- Todo el contenido de `agent-radar` pasó al pane (título del turno, fase y razón, tiempo, checklist, subagentes e historial); la banda sobre el prompt quedó en una línea con el nombre y los dos botones (detalle y ON/OFF). Así la banda no ocupa filas ni redibuja a 4 Hz, y el temporizador solo corre con el pane abierto. El pane sigue abriéndose solo con el botón.
- En terminal el pane no se colocaba: el botón esperaba una lectura de estado antes de abrir y el motor ya no lo trataba como una pulsación del usuario. Abrir como primera acción lo arregló, y el toast de fallo ahora da el motivo del motor. Probado a mano por el operador en terminal y escritorio; 92 tests.

## 2026-10-11 — ✅ Tarea 28 — Implementar pane para agent-radar

- `agent-radar` ganó un `Pane` de detalle que se abre y cierra solo con el botón `[ ◧ Detail ]` de la banda: checklist completo, subagentes vivos con su tarea completa y un historial (hasta 50) de los terminados, que la banda sigue retirando a los 5 s. Solo se abre por una pulsación porque un pane abierto por el mod bajo 144 columnas no se coloca; el contenido (detalle vivo más historial) lo eligió el operador.
- `session.end` ahora reinicia todo el estado del mod salvo ON/OFF. Probado a mano por el operador; 91 tests. Sin verificar con el motor real: el cierre por el usuario (hook `ui.close`, origen `person`) y cómo se acopla según la superficie.

## 2026-10-11 — ✅ Tarea 27 — Fusionar botones en usage-meter

- Los dos botones de vista de `usage-meter` (`[-] Compactar` y `[=] Una línea`) pasaron a uno solo que rota completa → compacta → una línea → completa y muestra la vista a la que pasará; el botón de idioma quedó aparte. Menos controles al pie y un orden predecible, a cambio de que volver a una vista concreta puede pasar por la intermedia.
- Fusionar también el idioma en ese botón se descartó por ser menos claro. Probado a mano por el operador; 65 tests.

## 2026-10-11 — ✅ Tarea 15 — Iniciar nuevo mod claude-radar

- Nació `agent-radar` (`mods/agent-radar/`, repo propio, aún sin remoto ni catálogo): un monitor pasivo sobre el prompt con el título del turno, su tiempo, el checklist de las tareas reales, la sección de subagentes con su nombre real y estado por `agentId`, y el botón `Claude Radar: ON/OFF` persistido en `$.store`. Oculta solo de forma visual las filas técnicas mientras trabaja y nunca toca la respuesta final; no hace llamadas a modelos ni registra comandos ni herramientas.
- El nombre pedido, `claude-radar`, está reservado por la validación (los plugins de terceros no pueden empezar con «claude-»), así que el id es `agent-radar` y el título visible sigue siendo «Claude Radar». El motor impone que `$` no cruce imports y que los `atom` vivan junto a su uso, por eso la lógica con `$` está en `register.tsx` y `claude-radar.tsx` queda puro. Probado a mano por el operador; 77 tests. Lo no verificable con el kit (p. ej. «Needs you» real) está en el README del mod.

## 2026-10-10 — ✅ Tarea 14 — Refinar el mod de caché

- En terminal con poco ancho el panel de `cache-watch` omite «se enfría en», y mientras el caché está caliente muestra cuántos tokens se reescribirían si se enfría (`en frío reescribe ~84k` en el panel, `~84k en juego` en la barra de estado). Importa porque lo que el operador quería saber era qué pierde si deja enfriar el caché; el recorte con poco ancho quita primero ese dato, luego «se enfría en».
- Se descartó mostrar el % de aciertos y un «ahorro» en dinero o límite: el mod no puede leer precios ni reglas de uso, y los mismos tokens ya dicen qué se evita. Probado a mano por el operador en parte; 74 tests.

## 2026-10-10 — ✅ Tarea 26 — Botón para cambiar a modo status en cache-watch

- El panel de `cache-watch` lleva un botón `[=] Barra de estado` alineado a la derecha, dentro del borde, que pasa a la vista `status`; en esa vista no hay botón porque la línea de estado es texto plano, y de vuelta a `panel` se va solo con `/cache-watch`. Evita tener que escribir el comando para el cambio más habitual.
- La alineación a la derecha necesitó que la caja interior ocupara todo el ancho (`flexGrow`); sin eso el botón quedaba pegado al texto. Probado a mano por el operador; 58 tests.

## 2026-10-10 — ✅ Tarea 24 — Refinamiento de UX

- `cache-watch` ganó una fila en blanco que lo separa del panel de `usage-meter` en la app de escritorio; en la terminal quedan pegados porque la banda ya va corta de filas. Un margen y una condición por `maxRows` no se veían en el escritorio, así que se usa una fila vacía según `e.surface`.
- El texto pasó a «Caché caliente» / «Caché fría» entera y coloreada, sin el `◆`; el contador es `59m 03s` (`1h 00m 00s` desde una hora) y la barra de estado omite el «se enfría en». Probado a mano por el operador en terminal y escritorio; 54 tests. Quedó aparte la Tarea 14 (información extra).

## 2026-10-10 — ✅ Tarea 23 — Cambiar cache-watch a la barra de estado

- `cache-watch` ahora tiene dos vistas, el panel sobre el prompt y la línea de estado del mod (`$.ui.status`), y el comando `/cache-watch` alterna entre ellas en vivo; la última elegida se recuerda entre sesiones (`$.store`) y manda sobre la opción `display`. Se quedó con las dos porque el operador quería poder elegir según el momento, no reemplazar el panel.
- Se probó un modo con colores ANSI en la línea de estado y se descartó: la línea de los mods es texto plano y los códigos salían rotos. Por eso la vista de barra no lleva colores y el panel conserva los suyos. Probado a mano por el operador (panel y barra, comando); 52 tests.

## 2026-10-10 — ✅ Tarea 22 — Borde gris oscuro en cache-watch y usage-meter

- Los paneles de `cache-watch` y `usage-meter` llevan el mismo borde redondeado gris oscuro (`#4b5563`) en todas las superficies, uno independiente por panel; antes solo la terminal lo tenía y el escritorio no. Se quitó la condición por superficie para que sea un solo comportamiento, y `usage-meter` ahora descuenta siempre lo que el borde ocupa.
- Verificado con tests (23 y 64) y `validate`; no se vio dibujado en una sesión real. Con la Tarea 23 (barra de estado) el borde de `cache-watch` podría dejar de aplicar.

## 2026-10-10 — ✅ Tarea 13 — Iniciar nuevo mod para mostrar el caché

- Nació `cache-watch` (repo `Gersom/claude-mod-cache-watch`, público, en el catálogo del central): una fila sobre el prompt que dice si el caché de prompts está caliente o frío, con cuenta regresiva y color/emoji según el calor que queda. Importa porque un caché frío obliga a reescribir toda la conversación, que gasta más tokens y límite.
- El motor no entrega el TTL (`5m`/`1h`) ni la hora de la última respuesta a los plugins: el TTL es una opción del mod (`1h` por defecto) y la hora se toma de los eventos del hilo principal. Para convivir con `usage-meter`, ambos piden primero lo que dibujan los demás y se apilan (`cache-watch` arriba); eso exigió un cambio en `usage-meter`.
- Los cambios de UX se probaron solo con tests (23 y 64), no en una sesión real. Los commits de UX y de `usage-meter` quedaron sin `git push`; la publicación inicial sí se hizo. Ajustes de UX e información extra: Tarea 14; borde gris: Tarea 22.

## 2026-10-10 — ✅ Tarea 12 — Subir el mod usage-meter al marketplace

- `usage-meter` quedó publicado en el catálogo del central `gersom-claude-mods` (fuente `github` hacia `Gersom/claude-mod-usage-meter`) y se instala de dos formas: con el central o suelto desde el repo del mod. Ambas se probaron en una configuración aislada, sin tocar la del operador; el operador confirmó que en la app de escritorio aparece en Plugins → Descubrir con el filtro Origen.
- Los README (central y mod) documentan la instalación en terminal y en la app de escritorio. No se probó instalar desde la propia app ni que el panel se dibuje con el plugin instalado desde el marketplace. Estructura en [`architecture.md`](../project/architecture.md).

## 2026-10-10 — ✅ Tarea 21 — Agregar LICENSE MIT al repo central

- El central `gersom-claude-mods` ahora lleva su `LICENSE` MIT (Gersom, 2026) y una sección «Licencia» en el README, que aclara que cada mod tiene la suya en su repo. Es lo que faltaba para que el repo público, que será el catálogo, tenga licencia explícita como los mods.

## 2026-10-10 — ✅ Tarea 20 — Preparar repo usage-meter para el marketplace

- `Gersom/claude-mod-usage-meter` quedó listo para publicarse: `LICENSE` MIT, versión 1.0.0 con `license`, `repository` y `homepage`, un `marketplace.json` de un plugin (nombre `usage-meter`) para instalarlo suelto, y README con la línea de instalación, el requisito de Claude Code 2.1.287+, la licencia y el enlace de donación.
- El plugin se queda en la raíz del repo (`source: "./"`, que valida) en lugar de moverlo a `src/`: con `src/` el `LICENSE` y el README de la raíz no viajarían con la instalación. `validate`, `--strict` y los 63 tests pasan; no se probó instalar desde GitHub en una sesión real (queda para la Tarea 12).

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
