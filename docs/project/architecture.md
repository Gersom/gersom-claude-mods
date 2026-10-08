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
├── docs/                        # documentación de contexto para agentes (este mapa)
├── AGENTS.md                    # orden de lectura para agentes (fuente de verdad)
└── CLAUDE.md                    # redirige a AGENTS.md
```

## Convenciones de organización

El repo es una colección de mods/skills para Claude Code; todavía no tiene código propio más allá del skill local. Cada mod nuevo debería vivir en su propia carpeta bajo `.claude/` (skills en `.claude/skills/<nombre>/`).

## Dónde va cada cosa nueva

- Un skill nuevo → `.claude/skills/<nombre>/` con su `SKILL.md`.
- Documentación de contexto del proyecto → `docs/`, según [`../README.md`](../README.md).
