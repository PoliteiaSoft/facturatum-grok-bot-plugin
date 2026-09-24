# Facturatum — complemento para ChatGPT

Complemento portable (Agent Plugins 1.0) de [Politeia Soft](https://politeiasoft.com) para operar **Facturatum** desde ChatGPT.

Servidor MCP remoto (OAuth, sin secretos en el paquete):

`https://gateway.politeiasoft.com/facturatum/mcp`

## Contenido

| Ruta | Uso |
|------|-----|
| `plugin.json` | Manifiesto Agent Plugins + metadata OpenAI |
| `mcp.json` | Servidor MCP con `type: streamable-http` |
| `skills/facturatum/SKILL.md` | Workflows y reglas de confirmación |
| `assets/` | Logo Facturatum y marca OpenAI de referencia |

## Importar en ChatGPT

1. Descarga `facturatum-chatgpt-plugin.zip` desde [Conectores](https://app.facturatum.es/conectores) o desde Docs (`/descargas/chatgpt-plugin/`).
2. En ChatGPT: **Ajustes → Complementos → Nuevo complemento** y sube el `.zip`.
3. Completa OAuth y elige la empresa en Facturatum.
4. En un chat nuevo, pide por ejemplo las últimas facturas recibidas.

Este paquete **no** es el plugin Cursor/Grok (carpeta `.cursor-plugin` en la raíz del repo). ChatGPT exige `type` en `mcp.json` y el esquema `agent-plugins.org`.

## Licencia

Uso del complemento ligado a una cuenta Facturatum activa.  
© Politeia Soft
