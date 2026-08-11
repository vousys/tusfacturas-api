---
description: >-
  API ARCA para emitir comprobantes con bonificaciones. Ideal para pymes que
  necesitan aplicar descuentos. Ejemplos incluidos. Confiable desde 2015. ¡Los
  desarrolladores la aman!
---

# Bonificaciones

En TusFacturasAPP existen **tres formas** de aplicar un descuento o bonificación a un comprobante:&#x20;

1\) A nivel producto, ingresando un porcentaje en el campo "bonificacion\_porcentaje" de cada concepto;&#x20;

2\) A nivel comprobante, ingresando un monto fijo en el campo "bonificacion" del bloque "comprobante";&#x20;

3\) O para casos que requieren mayor flexibilidad (como descuentos no atados a un producto puntual o valores que los campos de bonificación no permiten, por ejemplo importes negativos), enviando un concepto adicional en el bloque "detalle" con el campo "precio\_unitario\_sin\_iva" en negativo. A continuación se detalla cada una de estas opciones con ejemplos prácticos.

### ¿Cómo aplicar bonificaciones a nivel producto?

Para aplicar un descuento a un producto, simplemente ingresa el porcentaje deseado en el campo "bonificacion\_porcentaje" dentro de cada "producto" . Es importante tener en cuenta que las bonificaciones están sujetas al Impuesto al Valor Agregado (IVA).

**Ejemplo:**

Si un producto tiene un precio base de $100 y se aplica una bonificación del 20% con una alícuota de IVA del 21%, el cálculo sería el siguiente:

* Descuento: $100 \* 20% = $20
* Precio con descuento (sin IVA): $100 - $20 = $80
* Precio con descuento (con IVA): $100 - $20 = $80 \* 21%  = $96.80

### 1. Ejemplo de "Factura A" AFIP/ARCA con bonificación a nivel producto

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md" %}
[api-factura-electronica-afip-arca-factura-a-con-bonificacion.md](../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md)
{% endcontent-ref %}

### 2. Ejemplo de "Factura A" AFIP/ARCA con bonificación monetaria a nivel comprobante

Para aplicar un descuento a un comprobante, simplemente ingresa el monto exacto que deseas descontar en el campo "bonificacion" del bloque "comprobante".&#x20;

Es importante tener en cuenta que el Impuesto al Valor Agregado (IVA) se calcula sobre el subtotal luego de aplicar el descuento.

**Ejemplo:**

Si un producto tiene un precio base de $100 y se aplica una bonificación de $20 con una alícuota de IVA del 21%, el cálculo sería el siguiente:

* Precio con descuento (sin IVA): $100 - $20 = $80
* Precio con descuento (con IVA): $100 - $20 = $80 \* 21%  = $96.80

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md" %}
[api-factura-electronica-afip-arca-factura-a-con-bonificacion.md](../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md)
{% endcontent-ref %}

### 3. Ejemplo de concepto con importe unitario negativo

Además de las bonificaciones por producto o por comprobante, podés incluir un concepto adicional dentro del bloque `detalle` con el campo `precio_unitario_sin_iva` en negativo. Esto es útil cuando necesitás restar un importe puntual del total (por ejemplo, un ajuste, una devolución parcial o un descuento que no está asociado a ningún producto específico), ya que los campos `bonificacion` y `bonificacion_porcentaje` **no aceptan valores negativos**.

**Ejemplo:**

```json
// Some code
{
  ....
  "comprobante": {
    ..., 
    "detalle": [
      {
        "cantidad": "1",
        "afecta_stock": "N",
        "bonificacion_porcentaje": 0,
        "producto": {
          "descripcion": "Servicio de consultoría",
          "codigo": "SERV001",
          "lista_precios": "standard",
          "unidad_bulto": 1,
          "alicuota": 21,
          "precio_unitario_sin_iva": 1000
        }
      },
      {
        "cantidad": "1",
        "afecta_stock": "N",
        "bonificacion_porcentaje": 0,
        "producto": {
          "descripcion": "Ajuste / descuento comercial",
          "codigo": "AJUSTE001",
          "lista_precios": "standard",
          "unidad_bulto": 1,
          "alicuota": 21,
          "precio_unitario_sin_iva": -150
        }
      }
    ]
  }
}
```

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
