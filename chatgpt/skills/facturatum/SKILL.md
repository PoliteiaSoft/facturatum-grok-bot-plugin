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

1. `subir_pdf_factura_recibida` con `filename` + `contentBase64` (contenido del PDF en Base64). Si la factura ya existe, pasa `invoiceId` para adjuntarlo.
2. Si aún no hay factura: con el `fileId` devuelto, o bien:
   - `ejecutar_operacion` `POST /api/invoice-extraction/analyze-file` (query `fileId`) y luego `POST /api/received-invoices` con los datos + `fileId`, o
   - `POST /api/received-invoices/import-from-files` con `{ "fileIds": [<fileId>] }` si solo hay que dejarla pendiente.
3. No digas que «no se puede subir el PDF»: usa la tool. Máximo 10 MB.

## Errores

Si el MCP responde no autenticado, indica que debe reconectar desde `https://app.facturatum.es/conectores`. Si responde `not_found` o `forbidden`, explica el límite de permisos sin filtrar datos ajenos.
