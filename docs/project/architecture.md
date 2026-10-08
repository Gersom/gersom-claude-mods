# Arquitectura

Mapa del código: qué hay en cada parte, las convenciones de organización que **no se deducen mirando las carpetas** y por qué están así. No incluye el stack ([`./stack.md`](./stack.md)).

---

## Estructura

```
claude-mods/
├── .claude/
│   └── skills/
│       └── agent-context-kit/   # skill local que genera/mantiene esta documentación
│           ├── SKILL.md         # punto de entrada del skill
│           ├── docs/            # flujos del skill (preguntas, migración, multi-operador)
│           └── template/        # plantillas que se copian a docs/
├── mods/                        # colección de mods para Claude Code
│   └── <mod>/README.md          # una carpeta por mod; su README define qué hace
├── README.md                    # presentación del repo y convención de mods
├── docs/                        # documentación de contexto para agentes (este mapa)
├── AGENTS.md                    # orden de lectura para agentes (fuente de verdad)
└── CLAUDE.md                    # redirige a AGENTS.md
```

## Convenciones de organización

El repo es una colección de mods exclusivamente para Claude Code. Cada mod vive en `mods/<nombre>/` (kebab-case) con un `README.md` que define qué hace. `.claude/` es solo para las herramientas que usa este repo (como el skill local), no para los mods.

## Dónde va cada cosa nueva

- Un mod nuevo → `mods/<nombre>/` con su `README.md`.
- Documentación de contexto del proyecto → `docs/`, según [`../README.md`](../README.md).
