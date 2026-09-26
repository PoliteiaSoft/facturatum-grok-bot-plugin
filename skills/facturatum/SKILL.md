---
name: facturatum
description: Opera la empresa conectada en Facturatum (facturas emitidas y recibidas, contactos, cobros). Un solo trabajo: ejecutar la API del usuario vía MCP.
---

# Facturatum

## Trabajo

Ayudar al usuario a consultar y operar **su** empresa de Facturatum ya autorizada por OAuth. Empresa fijada en la conexión: no inventes otro `companyId`.

## Anti-trabajos

- No envíes, presentes, remeses, cobres ni borres sin confirmación explícita del usuario en este turno.
- No inventes importes, NIF ni números de factura.
- No pidas ni almacenes API keys: la autenticación es OAuth del conector.
- No cambies de empresa ni de tenant.

## Cómo trabajar

1. `listar_operaciones` para localizar el endpoint.
2. `describir_operacion` si hace falta el contrato.
3. `ejecutar_operacion` con `confirmacion: true` solo cuando el usuario lo haya pedido en este turno para una acción irreversible.

## Facturas recibidas con PDF

Cuando el usuario aporte un PDF (o diga «sube esta factura» con archivo):

1. Si el Base64 es **&lt; ~180 KB**: `subir_pdf_factura_recibida` con `filename` + `contentBase64` (y `invoiceId` si aplica).
2. Si es **mayor** (preferido): **no** metas el PDF en un tool call Base64.
   - `iniciar_subida_url_pdf_factura_recibida` con `filename` y `invoiceId` si aplica.
   - Con el `uploadUrl` devuelto, haz **POST HTTP** del fichero binario (multipart campo `file`, o body `application/pdf`). Sin JWT: el token va en la URL.
   - La respuesta del POST trae `fileId` / `attached`.
3. Fallback si no puedes POST HTTP: `iniciar_subida_pdf_factura_recibida` + `subir_parte_pdf_factura_recibida` (trozos raw ≤ 150 KB).
4. Si aún no hay factura: con el `fileId`, `ejecutar_operacion` analyze-file / create / import-from-files.
5. No digas que «no se puede subir el PDF». Máximo 10 MB. Requiere escritura de facturas recibidas.

## Errores

Si el MCP responde no autenticado, indica que debe **Desconectar** y **Reconectar** desde `https://app.facturatum.es/conectores`. Si responde `not_found` o `forbidden`, explica el límite de permisos sin filtrar datos ajenos.
