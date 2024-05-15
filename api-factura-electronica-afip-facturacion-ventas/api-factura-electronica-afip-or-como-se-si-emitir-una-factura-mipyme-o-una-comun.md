---
description: >-
  Si el monto de la factura que vas a emitir supera el tope impuesto por AFIP,
  es probable que debas emitir una factura de crédito electrónica MiPyme
---

# ¿Cómo determino si emitir una factura mipyme, o una factura común?

### Sugerencias para manejarlo desde tu plataforma:

### **1) Controlar el response de las facturas comúnes con error | "requiere\_fec" = "S"**

Si envías una factura A, B o C común y recibis error, verás que dentro del response existe un campo llamado: <mark style="color:purple;">**requiere\_fec**</mark>, si el contenido está en "SI", significa que debes emitirle a tu cliente una fc mipyme. En ese caso,  cambias el tipo de comprobante al mipyme que corresponda según la[ tabla de referencia](../parametros/tablas-de-referencia.md#tipos-de-comprobantes), y volves a enviar el request.[ Conocé más desde aquí](./#como-determinar-si-debo-emitir-un-comprobante-de-tipo-mipyme)\


### **2) Usar el método previo de consulta: "Éstoy obligado a emitir una FEC", antes de enviar a facturar**

Usando [este método](api-factura-electronica-afip-consulta-de-obligado-a-recibir-factura-de-credito-electronica-mipyme.md) obtendrás la respuesta directa desde AFIP en base a la consulta que realices.



TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).
