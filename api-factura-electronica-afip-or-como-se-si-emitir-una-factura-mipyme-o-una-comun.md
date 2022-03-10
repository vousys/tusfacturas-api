---
description: >-
  Si el monto de la factura que vas a emitir supera los $100,000 (éste monto
  varia muy frecuentemente y es gestionado por AFIP), es probable que debas
  emitir una factura de crédito electrónica MiPyme
---

# API Factura electrónica AFIP | ¿Cómo se si emitir una factura mipyme o una común?

### Sugerencias para manejarlo desde tu plataforma:



**1) Controlar el response de las facturas comúnes con error |  "requiere\_fec" = "S"**

Si envías una factura y viene con error, en el response vas a recibir un campo que se llama requiere\_fec, si está en  "SI", debes emitirle una fc mipyme. En ese caso, le cambias el tipo de comprobante al mipyme que corresponda, y volves a enviar el request. [https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante\
](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante)\
**2) Usar el método previo de consulta: "Éstoy obligado a emitir una FEC", antes de enviar a facturar**

Usando éste método, obtendrás la respuesta en base a la consulta que realices: [https://developers.tusfacturas.app/api-factura-electronica-afip-consulta-de-obligado-a-recibir-factura-de-credito-electronica-mipyme](https://developers.tusfacturas.app/api-factura-electronica-afip-consulta-de-obligado-a-recibir-factura-de-credito-electronica-mipyme)&#x20;

