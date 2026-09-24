# Facturatum — plugins MCP (Grok / Cursor y ChatGPT)

Plugins oficiales de [Politeia Soft](https://politeiasoft.com) para operar **Facturatum** vía MCP OAuth.

Servidor MCP remoto (OAuth, sin secretos en el repo):

`https://gateway.politeiasoft.com/facturatum/mcp`

## Dos formatos

| Carpeta | Cliente | Formato |
|---------|---------|---------|
| Raíz (`.cursor-plugin/`, `mcp.json`, `skills/`) | Grok Bot / Cursor | `.cursor-plugin` |
| [`chatgpt/`](./chatgpt/) | ChatGPT | Agent Plugins portable (`plugin.json` + `mcp.json` con `type`) |

No basta renombrar el plugin Cursor para ChatGPT: el MCP portable exige `"type": "streamable-http"`.

## Contenido (Grok / Cursor)

| Ruta | Uso |
|------|-----|
| `.cursor-plugin/plugin.json` | Manifiesto del plugin |
| `mcp.json` | Servidor MCP remoto |
| `skills/facturatum/SKILL.md` | Un trabajo, anti-trabajos y confirmación en acciones irreversibles |
| `assets/` | Logos de referencia (Grok, ChatGPT, Claude, DeepSeek) |
| `chatgpt/` | Complemento ChatGPT (ver su README) |

## Prueba local

1. Copia este repositorio a `~/.cursor/plugins/local/facturatum`  
   (Windows: `%USERPROFILE%\.cursor\plugins\local\facturatum`).
2. Recarga Cursor o Grok Bot.
3. Autoriza la empresa cuando el flujo OAuth abra  
   `https://app.facturatum.es/conectar/grok`  
   (o entra antes por `https://app.facturatum.es/conectores`).
4. En el chat, pide por ejemplo las últimas facturas recibidas.

## Publicar en el Marketplace (plugins)

1. Usa este repositorio público como origen.
2. Envía el plugin en https://cursor.com/marketplace/publish
3. Tras la aprobación, aparece en el Marketplace de Grok Bot → Plugins.

Este paquete es un **plugin de herramientas/MCP**, no un Bot template del catálogo de `x.ai/bot/marketplace`.

## Licencia

Uso del plugin ligado a una cuenta Facturatum activa.  
© Politeia Soft
