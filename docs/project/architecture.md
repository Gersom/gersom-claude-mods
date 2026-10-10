# Arquitectura

Mapa del código: qué hay en cada parte, las convenciones de organización que **no se deducen mirando las carpetas** y por qué están así. No incluye el stack ([`./stack.md`](./stack.md)).

---

## Estructura

```
gersom-claude-mods/                # repo central (GitHub: Gersom/gersom-claude-mods)
├── .claude/
│   └── skills/
│       └── agent-context-kit/     # skill local que genera/mantiene esta documentación
│           ├── SKILL.md           # punto de entrada del skill
│           ├── docs/              # flujos del skill (preguntas, migración, multi-operador)
│           └── template/          # plantillas que se copian a docs/
├── .claude-plugin/
│   └── marketplace.json           # catálogo de mods (marketplace «gersom-claude-mods»)
├── mods/                          # ignorada por git: cada subcarpeta es un repo propio
│   └── usage-meter/               # recuadro con % de contexto y límites de 5 h y semanal
├── README.md                      # presentación del central e instalación
├── docs/                          # documentación de contexto para agentes (este mapa)
├── AGENTS.md                      # orden de lectura para agentes (fuente de verdad)
└── CLAUDE.md                      # redirige a AGENTS.md
```

## Convenciones de organización

El repo es el **central** de una colección de mods exclusivamente para Claude Code. Cada mod es un repo propio, clonado en `mods/<nombre>/` (kebab-case) con su `README.md` que define qué hace; `mods/` está en `.gitignore`, así que el central no versiona los mods pero se pueden leer y editar desde acá. El catálogo es `.claude-plugin/marketplace.json`, con una entrada por mod y fuente `github`. `.claude/` es solo para las herramientas que usa este repo (como el skill local), no para los mods.

Mientras un mod no tenga su repo propio, sus archivos siguen versionados en el central (hoy, `usage-meter`; ver Tarea 19 en [`backlog.md`](../agents/backlog.md)).

## Dónde va cada cosa nueva

- Un mod nuevo → repo propio en `mods/<nombre>/` con su `README.md`, y una entrada en `.claude-plugin/marketplace.json`.
- Documentación de contexto del proyecto → `docs/`, según [`../README.md`](../README.md).
- Cómo se hacen los commits entre repos → regla «Cada mod es un repo aparte» en [`../agents/rules.md`](../agents/rules.md).
