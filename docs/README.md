# gersom-claude-mods

Repo central de los mods de Claude Code de Gersom: contiene el catálogo (marketplace) y la documentación; cada mod vive en su propio repo dentro de `mods/`.

**Operador:** la persona dueña del proyecto que le pide tareas al agente, aprueba decisiones y a quien se le pregunta cuando algo no está definido.

## Mapa de `docs/`

```
docs/
├── agents/
│   ├── rules.md          # reglas fijas del proyecto
│   ├── handoff.md        # estado actual del trabajo
│   ├── backlog.md        # tareas pendientes
│   └── history.md        # tareas cerradas y por qué
└── project/
    ├── architecture.md   # estructura del código y dónde va cada cosa nueva
    └── decisions/
        ├── README.md     # índice de decisiones técnicas, un archivo por tema
        └── stack.md      # decisiones de stack que no se ven en las dependencias
```

Para ubicarte en el código o saber dónde va algo nuevo: [`project/architecture.md`](./project/architecture.md).
