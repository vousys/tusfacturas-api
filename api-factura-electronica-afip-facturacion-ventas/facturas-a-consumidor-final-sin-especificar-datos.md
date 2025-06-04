---
description: >-
  TusFacturasAPP es un software de facturación y un software de gestión 
  diseñado para empresas que facturen en Argentina. Conoce más de
  TusFacturasAPP.
---

# Facturas a consumidor final, sin especificar datos

Si queres facturar un comprobante **a consumidor final, sin especificar su nombre y DNI**, debes enviar dentro del bloque "cliente" >  campo "tipo" y "número"  de documento, lo siguiente:

Nro de documento = "0"

Tipo de documento = "OTRO"



Podes consultar diariamente el limite establecido por AFIP hasta el cual podrás emitir éste tipo de comprobantes, usando nuestro servicio API:

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final.md" %}
[api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final.md](../web-services-afip-api-arca/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final.md)
{% endcontent-ref %}

Es responsabilidad del emisor verificar la concordancia entre el medio de pago y la factura, ya que la AFIP asume que las facturas electrónicas se emiten mediante medios de pago electrónicos. La condición de venta no se transmite a través de los webservices de la AFIP.

### Ejemplo:

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-factura-b-sin-especificar-comprador.md" %}
[api-factura-electronica-afip-factura-b-sin-especificar-comprador.md](../web-services-afip-api-arca/api-factura-electronica-afip-factura-b-sin-especificar-comprador.md)
{% endcontent-ref %}



{% hint style="info" %}
Datos a tener en cuenta:



* En nombre y dirección, indicá lo que tu contador/a te recomiende. Según la provincia que selecciones los contadores luego tienen que hacer la declaración de Ingresos Brutos. Desde el lado técnico de la plataforma se requiere un texto.
* Solo podrás facturar "sin indicar el documento del comprador" hasta ciertos montos, ya que AFIP/ARCA actualiza éste dato regularmente. TusFacturasAPP cuenta con un método que podes consultar 1 vez por día que te permite obtener el monto actualizado. [Consultá la documentación: los topes de venta a CF](https://developers.tusfacturas.app/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final) &#x20;
{% endhint %}

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
