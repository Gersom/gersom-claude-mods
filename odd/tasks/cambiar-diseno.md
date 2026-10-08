# Cambiar diseño del panel de uso (Tarea 4)

## Objetivo
Rediseñar solo la interfaz visual del mod `usage-meter`, sin cambiar obtención de datos, cálculos ni frecuencia de actualización.

## Alcance
- `mods/usage-meter/hooks/format.ts`: funciones de presentación.
- `mods/usage-meter/hooks/register.tsx`: layout, colores y animación.
- `mods/usage-meter/hooks/*.test.ts`: tests.
- `mods/usage-meter/README.md`: documentar el diseño nuevo.

Fuera de alcance: botones, métricas nuevas, cambios de datos, umbrales (Tarea 5).

## Modo TDD
Ni activo ni configurado en el proyecto: ejecutar pruebas funcionales (`claude plugin test`, `claude plugin validate`).

## Checklist
- [x] T4.0 Mover la tarea del backlog a `handoff.md` y crear este documento.
- [ ] T4.1 `format.ts`: presentación (bloques vacíos en gris, porcentaje alineado, reset atenuado).
- [ ] T4.2 `register.tsx`: layout nuevo (título gris suave, color distintivo en etiqueta y barra, reset en segunda línea si no cabe).
- [ ] T4.3 Animación de la barra y del porcentaje con `$.clock.every`; sin animación si el valor no cambia.
- [ ] T4.4 Tests de `format.ts` y `register.tsx`.
- [ ] T4.5 `claude plugin validate` y `claude plugin test` sobre `mods/usage-meter`.
- [ ] T4.6 README y cierre (`history.md`, `handoff.md`, `backlog.md`).

## Decisiones
- Color distintivo: contexto azul; límites violeta.
- Barra en reposo: color por umbral (verde/amarillo/rojo). Durante la animación: color distintivo; al terminar vuelve al color del umbral.
- Terminal estrecha: reset en segunda línea.
- Solo tema oscuro.
- Umbrales 70/90 sin cambio (ver Tarea 5).

## Progreso
- T4.0 completada.

## Próximo paso
T4.1: `format.ts`.
