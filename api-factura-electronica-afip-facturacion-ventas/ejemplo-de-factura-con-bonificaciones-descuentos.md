---
description: >-
  API ARCA para emitir comprobantes con bonificaciones. Ideal para pymes que
  necesitan aplicar descuentos. Ejemplos incluidos. Confiable desde 2015. ¡Los
  desarrolladores la aman!
---

# Bonificaciones

### ¿Cómo aplicar bonificaciones a nivel producto?

Para aplicar un descuento a un producto, simplemente ingresa el porcentaje deseado en el campo "bonificacion\_porcentaje" dentro de cada "producto" . Es importante tener en cuenta que las bonificaciones están sujetas al Impuesto al Valor Agregado (IVA).

**Ejemplo:**

Si un producto tiene un precio base de $100 y se aplica una bonificación del 20% con una alícuota de IVA del 21%, el cálculo sería el siguiente:

* Descuento: $100 \* 20% = $20
* Precio con descuento (sin IVA): $100 - $20 = $80
* Precio con descuento (con IVA): $100 - $20 = $80 \* 21%  = $96.80

### Ejemplo de "Factura A" AFIP/ARCA con bonificación a nivel producto

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md" %}
[api-factura-electronica-afip-arca-factura-a-con-bonificacion.md](../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md)
{% endcontent-ref %}

### Ejemplo de "Factura A" AFIP/ARCA con bonificación monetaria a nivel comprobante

Para aplicar un descuento a un comprobante, simplemente ingresa el monto exacto que deseas descontar en el campo "bonificacion" del bloque "comprobante".&#x20;

Es importante tener en cuenta que el Impuesto al Valor Agregado (IVA) se calcula sobre el subtotal luego de aplicar el descuento.

**Ejemplo:**

Si un producto tiene un precio base de $100 y se aplica una bonificación de $20 con una alícuota de IVA del 21%, el cálculo sería el siguiente:

* Precio con descuento (sin IVA): $100 - $20 = $80
* Precio con descuento (con IVA): $100 - $20 = $80 \* 21%  = $96.80

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md" %}
[api-factura-electronica-afip-arca-factura-a-con-bonificacion.md](../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md)
{% endcontent-ref %}



TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
