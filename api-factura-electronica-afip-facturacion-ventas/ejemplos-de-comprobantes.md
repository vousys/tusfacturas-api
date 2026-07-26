---
description: >-
  API AFIP para emitir facturas electrónicas AFIP. Ejemplos de facturas A, B, C,
  notas de crédito y débito. Confiable desde 2015. ¡Los desarrolladores la aman!
---

# Como confeccionar una venta

TusFacturasAPP ofrece tres modalidades para emitir comprobantes a través de la API REST ARCA. Elegí la que mejor se adapte a tu arquitectura e integrala en minutos.

**Facturación asincrónica (recomendada)**

El comprobante se encola y se emite en segundo plano. Recibís la confirmación vía webhook una vez procesado. No depende del estado de los servicios de ARCA en el momento del request, por lo que es la opción más robusta para entornos de producción.

👉 [Ver documentación: facturación asincrónica](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1)

**Facturación instantánea**

El comprobante se emite en el momento y recibís la respuesta de forma inmediata. Depende del estado de los servicios de ARCA: si ARCA no responde, el request será rechazado.

👉 [Ver documentación: facturación instantánea](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante)

**Facturación por lotes**

Permite enviar múltiples comprobantes en un solo request para procesarlos simultáneamente. Ideal para alto volumen.

👉 [Ver documentación: facturación por lotes](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-api-facturacion-por-lotes)

***

**¿Buscas ejemplos de JSON listos para usar?**

Accede a la colección de ejemplos por tipo de comprobante: Facturas A, B, C, E, MiPyME, notas de crédito, notas de débito, facturas en dólares, con bonificaciones y más.

👉 [Ver ejemplos por tipo de comprobante](https://developers.tusfacturas.app/web-services-afip-api-arca)
