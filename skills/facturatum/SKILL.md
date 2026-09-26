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

1. Calcula el tamaño del Base64. Si es **&lt; ~180 KB**, usa `subir_pdf_factura_recibida` con `filename` + `contentBase64` (y `invoiceId` si la factura ya existe).
2. Si el Base64 es **mayor** (límite típico del cliente ~700 KB): **no** intentes un solo argumento enorme.
   - `iniciar_subida_pdf_factura_recibida` con `filename`, `totalParts`, y `invoiceId` si aplica (`totalBytes` opcional).
   - Luego `subir_parte_pdf_factura_recibida` por cada parte en orden (`partNumber` 1-based, `contentBase64`). Cada trozo **raw ≤ 150 KB** (~200 KB Base64).
   - La última parte responde con `fileId` / `attached` como el upload monolítico.
3. Si aún no hay factura: con el `fileId` devuelto, o bien:
   - `ejecutar_operacion` id=`POST /api/invoice-extraction/analyze-file` (query `fileId`) y luego `ejecutar_operacion` id=`POST /api/received-invoices` con los datos + `fileId`, o
   - `ejecutar_operacion` id=`POST /api/received-invoices/import-from-files` con body `{ "fileIds": [<fileId>] }` si solo hay que dejarla pendiente.
4. No digas que «no se puede subir el PDF»: usa la tool adecuada. Máximo 10 MB del PDF. Requiere permiso de escritura de facturas recibidas.

## Errores

Si el MCP responde no autenticado, indica que debe **Desconectar** y **Reconectar** desde `https://app.facturatum.es/conectores`. Si responde `not_found` o `forbidden`, explica el límite de permisos sin filtrar datos ajenos.
