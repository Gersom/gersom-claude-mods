# Cambiar diseño del panel de uso (Tarea 4)

## Objetivo
Rediseñar solo la interfaz visual del mod `usage-meter`, sin cambiar obtención de datos, cálculos ni frecuencia de actualización.

## Alcance
- `mods/usage-meter/hooks/format.ts`: funciones de presentación.
- `mods/usage-meter/hooks/register.tsx`: layout, colores y animación.
- `mods/usage-meter/types/index.d.ts`: valor `shown` en el contrato de estado.
- `mods/usage-meter/hooks/*.test.ts`: tests.
- `mods/usage-meter/README.md`: documentar el diseño nuevo.

Fuera de alcance: botones, métricas nuevas, cambios de datos, umbrales (Tarea 5).

## Modo TDD
Ni activo ni configurado en el proyecto: ejecutar pruebas funcionales (`claude plugin test`, `claude plugin validate`).

## Checklist
- [x] T4.0 Mover la tarea del backlog a `handoff.md` y crear este documento.
- [x] T4.1 `format.ts`: `barParts`, `rowsOf`, `withPercent`, `inlineFits`, colores de acento. Commit `62492c1`.
- [x] T4.2 `register.tsx`: título gris, etiqueta y barra en color distintivo, barra vacía en gris tenue, reset en segunda línea si no cabe. Commit `62492c1`.
- [x] T4.3 Animación con `$.clock.every` sobre `$.state` (`shown`); sin animación si el valor no cambia. Commit `62492c1`.
- [x] T4.4 Tests de `format.ts` actualizados (`barParts`, `rowsOf`, `withPercent`, `inlineFits`). Tests de `register.tsx` sin cambios.
- [x] T4.5 `claude plugin validate mods/usage-meter`: pasó. `claude plugin test mods/usage-meter`: 23 pasan, 0 fallan.
- [x] T4.6 README y cierre (`history.md`, `handoff.md`). Cierre pedido por el operador tras revisión en sesión.

## Pendiente de verificar
- La animación y los colores no se vieron en una sesión real. Los tests no cubren la animación.
- Los nombres de color (`#60a5fa` azul, `#a78bfa` violeta, `gray`, `red`, `yellow`, `green`) se comprobarán en la sesión en tema oscuro.

## Decisiones
- Color distintivo: contexto azul (`#60a5fa`); límites violeta (`#a78bfa`). La especificación daba verde o violeta; se eligió violeta para no confundirlo con el verde del umbral.
- Barra en reposo: color por umbral (verde/amarillo/rojo). Durante la animación: color distintivo; al terminar vuelve al color del umbral.
- El porcentaje no cambia de color.
- Terminal estrecha: el reset pasa a una segunda línea (ya no se recorta).
- Solo tema oscuro; no se contempla el claro.
- Umbrales 70/90 sin cambio (ver Tarea 5).

## Progreso
- Commits en `feat/cambiar-diseno`:
  - `62492c1` feat(T-4): rediseñar panel de uso con colores por métrica y animación
  - `8b7e504` docs(T-4): registrar avance de cambiar diseño y tarea de porcentajes

## Próximo paso
Revisar el panel en una sesión real (tema oscuro): colores, animación y reset en terminal estrecha. Después, si el operador lo pide, cerrar la tarea (T4.6).
