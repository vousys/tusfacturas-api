---
description: >-
  API ARCA para emitir comprobantes con bonificaciones. Ideal para pymes que
  necesitan aplicar descuentos. Ejemplos incluidos. Confiable desde 2015. ¡Los
  desarrolladores la aman!
icon: percent
---

# Bonificaciones

En TusFacturasAPP existen **tres formas** de aplicar un descuento o bonificación a un comprobante:

<table><thead><tr><th width="106.7109375"></th><th width="250.95703125">A nivel producto</th><th>A nivel comprobante</th><th width="241.44140625">Concepto negativo</th></tr></thead><tbody><tr><td><strong>Campo</strong></td><td><code>bonificacion_porcentaje</code></td><td><code>bonificacion</code></td><td><code>precio_unitario_sin_iva</code> (en negativo)</td></tr><tr><td><strong>Bloque</strong></td><td><code>detalle</code> (en cada concepto)</td><td><code>comprobante</code></td><td><code>detalle</code> (como un concepto más)</td></tr><tr><td><strong>Valor</strong></td><td>Porcentaje</td><td>Monto fijo</td><td>Monto fijo negativo</td></tr><tr><td><strong>Se descuenta de</strong></td><td>El precio unitario de ese producto</td><td>El subtotal sin IVA de la alícuota 21%</td><td>El subtotal de la alícuota que le asignes al concepto</td></tr><tr><td><strong>IVA</strong></td><td>Se calcula sobre el precio ya descontado</td><td>Se calcula sobre el subtotal ya descontado</td><td>Se calcula sobre el subtotal ya descontado</td></tr><tr><td><strong>Cuándo usarla</strong></td><td>Descuento sobre un producto puntual</td><td>Descuento general, si todos los ítems son al 21%</td><td>Descuentos no atados a un producto, ajustes y redondeos</td></tr></tbody></table>

> **Si tu comprobante tiene varias alícuotas**, la bonificación a nivel comprobante se aplica solo sobre el subtotal al 21%. Para descontar sobre otra alícuota, usá un concepto negativo.
>
> Los campos `bonificacion` y `bonificacion_porcentaje` no aceptan valores negativos.

### **Bonificación a nivel producto**

&#x20;ingresando un porcentaje en el campo `bonificacion_porcentaje` de cada concepto del bloque `detalle`. El descuento se aplica sobre el precio unitario de ese producto sin IVA y el IVA se calcula sobre el precio con la bonificación ya descontada.

Ejemplo:

| Concepto                         | Cálculo      | Importe    |
| -------------------------------- | ------------ | ---------- |
| Precio unitario sin IVA          |              | $100,00    |
| Bonificación (20%)               | $100 × 20%   | −$20,00    |
| **Precio con descuento sin IVA** | $100 − $20   | **$80,00** |
| IVA 21%                          | $80 × 21%    | $16,80     |
| **Precio con descuento con IVA** | $80 + $16,80 | **$96,80** |

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md" %}
[api-factura-electronica-afip-arca-factura-a-con-bonificacion.md](../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md)
{% endcontent-ref %}

***

### **Bonificación nivel comprobante**

Ingresando un monto fijo en el campo `bonificacion` del bloque `comprobante`. El monto ingresado se descuenta del **primer subtotal sin IVA**, que corresponde a la alícuota del **21%**. Si tu comprobante tiene ítems con distintas alícuotas, tené en cuenta que la bonificación se aplica únicamente sobre ese subtotal. El IVA se calcula sobre el subtotal resultante luego de aplicar el descuento.

Ejemplo:

Este ejemplo tiene un ítem al 21% y otro al 10,5%. La bonificación a nivel comprobante se descuenta solo del subtotal al 21%:

| Concepto                      | Alícuota 21%       | Alícuota 10,5%      |
| ----------------------------- | ------------------ | ------------------- |
| Producto A                    | $100,00            |                     |
| Producto B                    |                    | $50,00              |
| **Subtotal sin IVA**          | $100,00            | $50,00              |
| Bonificación (`bonificacion`) | −$20,00            | —                   |
| **Subtotal con descuento**    | **$80,00**         | **$50,00**          |
| IVA                           | $80 × 21% = $16,80 | $50 × 10,5% = $5,25 |
| **Total por alícuota**        | $96,80             | $55,25              |

**Total del comprobante: $96,80 + $55,25 = $152,05**

> Los $20 de bonificación se descuentan solo del subtotal al 21%. El subtotal al 10,5% no cambia. Si necesitás aplicar un descuento sobre otra alícuota, usa un concepto con importe negativo.

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md" %}
[api-factura-electronica-afip-arca-factura-a-con-bonificacion.md](../web-services-afip-api-arca/api-factura-electronica-afip-arca-factura-a-con-bonificacion.md)
{% endcontent-ref %}

***

### **Bonificación mediante un concepto con importe negativo:**&#x20;

para casos que requieren mayor flexibilidad, como descuentos no atados a un producto puntual o ajustes que los campos anteriores no permiten (por ejemplo, importes que no corresponden a un porcentaje exacto), podés enviar un concepto adicional en el bloque `detalle` con el campo `precio_unitario_sin_iva` en negativo. Esta es la opción más flexible ya que no tiene las restricciones de los campos `bonificacion` y `bonificacion_porcentaje`, que **no aceptan valores negativos**.

**Importante:** ARCA no permite emitir comprobantes con sub-totales negativos para las alícuotas «IVA No Gravado» o «Exento». Por este motivo, no podrás informar un ajuste negativo (por ejemplo, -$0,05) utilizando alguna de estas alícuotas, si no existe otro ítem de la misma alícuota que permita compensar ese importe y mantener el subtotal en cero o positivo.

### 3. Ejemplo de concepto con importe unitario negativo

Además de las bonificaciones por producto o por comprobante, podés incluir un concepto adicional dentro del bloque `detalle` con el campo `precio_unitario_sin_iva` en negativo. Esto es útil cuando necesitás restar un importe puntual del total (por ejemplo, un ajuste, una devolución parcial o un descuento que no está asociado a ningún producto específico), ya que los campos `bonificacion` y `bonificacion_porcentaje` **no aceptan valores negativos**.

Ejemplo:

En este ejemplo se aplica un descuento de $10 solo sobre la alícuota del 10,5%. Con el campo `bonificacion` no se podría, porque descuenta del 21%.

| Concepto               | Cantidad | `precio_unitario_sin_iva` | Alícuota 21%        | Alícuota 10,5%      |
| ---------------------- | -------- | ------------------------- | ------------------- | ------------------- |
| Producto A             | 1        | 100,00                    | $100,00             |                     |
| Producto B             | 1        | 50,00                     |                     | $50,00              |
| Descuento especial     | 1        | **−10,00**                |                     | −$10,00             |
| **Subtotal sin IVA**   |          |                           | **$100,00**         | **$40,00**          |
| IVA                    |          |                           | $100 × 21% = $21,00 | $40 × 10,5% = $4,20 |
| **Total por alícuota** |          |                           | $121,00             | $44,20              |

**Total del comprobante: $121,00 + $44,20 = $165,20**

> El concepto negativo se resta del subtotal de **la alícuota que le asignes**, y el IVA se calcula sobre el subtotal ya descontado. Por eso sirve para descuentos sobre cualquier alícuota, ajustes o redondeos.

***

{% content-ref url="redondeos.md" %}
[redondeos.md](redondeos.md)
{% endcontent-ref %}





### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
