---
description: >-
  API ARCA para emitir comprobantes con bonificaciones. Ideal para pymes que
  necesitan aplicar descuentos. Ejemplos incluidos. Confiable desde 2015. ¡Los
  desarrolladores la aman!
icon: percent
---

# Bonificaciones

En TusFacturasAPP existen **tres formas** de aplicar un descuento o bonificación a un comprobante:

**1) A nivel producto:** ingresando un porcentaje en el campo `bonificacion_porcentaje` de cada concepto del bloque `detalle`. El descuento se aplica sobre el precio unitario de ese producto y el IVA se calcula sobre el precio ya descontado.

**2) A nivel comprobante:** ingresando un monto fijo en el campo `bonificacion` del bloque `comprobante`. El monto ingresado se descuenta del **primer subtotal sin IVA**, que corresponde a la alícuota del **21%**. Si tu comprobante tiene ítems con distintas alícuotas, tené en cuenta que la bonificación se aplica únicamente sobre ese subtotal. El IVA se calcula sobre el subtotal resultante luego de aplicar el descuento.

**3) Mediante un concepto con importe negativo:** para casos que requieren mayor flexibilidad, como descuentos no atados a un producto puntual o ajustes que los campos anteriores no permiten (por ejemplo, importes que no corresponden a un porcentaje exacto), podés enviar un concepto adicional en el bloque `detalle` con el campo `precio_unitario_sin_iva` en negativo. Esta es la opción más flexible ya que no tiene las restricciones de los campos `bonificacion` y `bonificacion_porcentaje`, que **no aceptan valores negativos**.

A continuación se detalla cada una de estas opciones con ejemplos prácticos.

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

Para aplicar un descuento a un comprobante, ingresá el monto exacto que querés descontar en el campo `bonificacion` del bloque `comprobante`.

⚠️ **Importante:** la bonificación general monetaria se aplica al **primer subtotal sin IVA**, que corresponde a la alícuota del **21%**. Si tu comprobante tiene ítems con distintas alícuotas de IVA (por ejemplo, algunos al 21% y otros exentos o al 10.5%), la bonificación se descontará únicamente del subtotal correspondiente al 21%. Tené esto en cuenta al calcular el descuento que necesitás aplicar.

El IVA se calcula sobre el subtotal **luego de aplicar el descuento**.

**Ejemplo:**

Si un producto tiene un precio base de $100 y se aplica una bonificación de $20 con una alícuota de IVA del 21%, el cálculo sería el siguiente:

* Precio con descuento (sin IVA): $100 - $20 = $80
* IVA 21% sobre $80: $16.80
* **Precio final con IVA: $96.80**

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
