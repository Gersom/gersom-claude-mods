# gersom-claude-mods

Colección de mods de Gersom, exclusivamente para Claude Code. Este repo es el **central**: su `.claude-plugin/marketplace.json` es el catálogo y cada mod vive en su propio repo.

## Instalar

Agregar el marketplace una sola vez:

```
/plugin marketplace add Gersom/gersom-claude-mods
```

Después, instalar el mod que se quiera, por nombre:

```
/plugin install <mod>@gersom-claude-mods
```

Cada mod se instala por separado y se actualiza desde su propio repo.

## Mods

| Mod | Qué hace | Repo |
|---|---|---|
| `usage-meter` | Recuadro sobre el prompt con el % de contexto y de los límites de 5 horas y semanal. | [claude-mod-usage-meter](https://github.com/Gersom/claude-mod-usage-meter) |

## Para quien desarrolla

- Cada mod es un repo propio en `mods/<nombre>/` (`kebab-case`), con su `.git`; esta carpeta está en `.gitignore` y este repo no versiona los mods.
- El `README.md` de cada mod es obligatorio y define qué hace.
- Para agregar un mod al catálogo: una entrada en `plugins` de `.claude-plugin/marketplace.json` con `source` de tipo `github`.
- Documentación de contexto para agentes: [`docs/README.md`](./docs/README.md).

## Licencia

[MIT](./LICENSE) © Gersom. Cada mod lleva su propia licencia en su repo.
