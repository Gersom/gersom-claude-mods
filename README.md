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

### En la app de escritorio

1. Agregar el marketplace: **Configuración → Plugins → Añadir → Añadir marketplace → Añadir desde un repositorio**, pegar la URL del repo (`https://github.com/Gersom/gersom-claude-mods`) y pulsar **Sincronizar**.
2. Encontrar los mods: en **Plugins → Descubrir**, abrir el filtro y elegir **Origen → `gersom-claude-mods`**. Los mods del catálogo aparecen listados y se instalan desde ahí.

## Mods

| Mod | Qué hace | Repo |
|---|---|---|
| `usage-meter` | Recuadro sobre el prompt con el % de contexto y de los límites de 5 horas y semanal. | [claude-mod-usage-meter](https://github.com/Gersom/claude-mod-usage-meter) |
| `cache-watch` | Panel sobre el prompt que muestra si el caché de prompts está caliente o frío, con cuenta regresiva. | [claude-mod-cache-watch](https://github.com/Gersom/claude-mod-cache-watch) |

## Para quien desarrolla

- Cada mod es un repo propio en `mods/<nombre>/` (`kebab-case`), con su `.git`; esta carpeta está en `.gitignore` y este repo no versiona los mods.
- El `README.md` de cada mod es obligatorio y define qué hace.
- Para agregar un mod al catálogo: una entrada en `plugins` de `.claude-plugin/marketplace.json` con `source` de tipo `github`.
- Documentación de contexto para agentes: [`docs/README.md`](./docs/README.md).

## Licencia

[MIT](./LICENSE) © Gersom. Cada mod lleva su propia licencia en su repo.
