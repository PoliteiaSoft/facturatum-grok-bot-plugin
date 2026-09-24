# Facturatum — plugin para Grok Bot / Cursor

Plugin oficial de [Politeia Soft](https://politeiasoft.com) para operar **Facturatum** desde Grok Bot (mismo formato que los plugins de Cursor).

Servidor MCP remoto (OAuth, sin secretos en el repo):

`https://gateway.politeiasoft.com/facturatum/mcp`

## Contenido

| Ruta | Uso |
|------|-----|
| `.cursor-plugin/plugin.json` | Manifiesto del plugin |
| `mcp.json` | Servidor MCP remoto |
| `skills/facturatum/SKILL.md` | Un trabajo, anti-trabajos y confirmación en acciones irreversibles |
| `assets/` | Logos de referencia (Grok, ChatGPT, Claude, DeepSeek) |

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
