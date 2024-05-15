---
description: >-
  Emití con la API de TusFacturas.app notas de crédito y notas de débito A, B,
  C, M y MiPyme.
---

# Notas de crédito / Notas de débito

AFIP te permite emitir notas de crédito y notas de débito parciales o totales, detallando un comprobante en particular que se anula o hacerlo por períodos desde-hasta, para esto solo debes agregar los bloques: "comprobantes\_asociados" o "comprobantes\_asociados\_periodo" al JSON.

### ¿Qué es una nota de crédito (NC) electrónica?

Es un comprobante dígital legalmente equivalente a la [nota de crédito](https://www.tusfacturas.app/como-emitir-notas-de-credito-electronica-afip.html) en formato papel, que la reemplaza en la mayoría de las operaciones de quienes estén obligados u opten por su utilización.&#x20;

### ¿Qué es una nota de débito (ND) electrónica?

Es un comprobante dígital legalmente equivalente a la [nota de débito](https://www.tusfacturas.app/como-emitir-notas-de-debito-electronica-afip.html) en formato papel, que la reemplaza en la mayoría de las operaciones de quienes estén obligados u opten por su utilización.

### Emitir Notas de débito/crédito detallando los comprobantes que se anulan

Para éste tipo de información, es obligatorio enviar el detalle de los comprobantes que se anulan, dentro de un array, en el bloque llamado "**comprobantes\_asociados**", acorde a la estructura que se detalla a continuación para cada comprobante asociado.

{% hint style="info" %}
**Datos a tener en cuenta:**&#x20;

* Los comprobantes que se asocien deben haberse emitido en la misma moneda en que se esta emitiendo la nota de crédito/débito.
* La fecha del comprobante que asocies debe ser menor o igual a la fecha del comprobante que estas queriendo emitir. Tené en cuenta que AFIP realiza validaciones en cuanto a la fecha de los comprobantes que asocies, ya que no se permiten notas de crédito a comprobantes con  +15 días.



**Auto-acreditación en cuenta corriente:**

A partir del 26/03/2022, comienza a funcionar la "auto-acreditación" con las NC, solo si cumple con los siguientes requisitos:

1. Detalla un solo comprobante.&#x20;
2. El importe de la NC es exactamente igual al del comprobante que éstas anulando (factura o nota de débito).
3. La factura o nota de débito que estás anulando, se encuentra impaga al 100%.

La auto-acreditación generará un recibo de cobro, en la cuenta corriente de tu cliente, para anular contablemente esa factura o nota de débito asociada. No se enviará ningún PDF a tu cliente ni se enviará éste recibo de cobro a AIP. Esta información es solo para tu gestión interna dentro de nuestra plataforma.


{% endhint %}



Ejemplo del JSON a enviar:

```json
comprobante: {
   .... 
   ,comprobantes_asociados:[
           {
             "tipo_comprobante"   :    "FACTURA A",
              "punto_venta"  :    "145",
              "numero" : 12313,
              "comprobante_fecha": "07/07/2019",
              "cuit": 111111111     
            } ,
           {
             "tipo_comprobante"   :    "FACTURA A",
              "punto_venta"  :    "146",
              "numero" : 12314,
              "comprobante_fecha": "08/07/2019",
              "cuit": 111111111     
            } ,   
      ] 
  }
```

Información de los campos a enviar:

<table data-header-hidden><thead><tr><th></th><th width="140.66666666666669" align="center">REQUERIDO</th><th></th></tr></thead><tbody><tr><td><code>tipo_comprobante</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfabético. Valores esperados según <a href="../parametros/tablas-de-referencia.md#tipos-de-comprobantes">tabla de tipos de comprobante.</a></td></tr><tr><td><code>punto_venta</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico entero. Longitud máxima 5 digitos.<br><strong>Ejemplo: 3</strong></td></tr><tr><td><code>numero</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></td></tr><tr><td><code>cuit</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico, sin puntos ni guiones. Es el CUIT de quien emitió el comprobante asociado. Siempre debe ser el mismo de quien está facturando.<br><strong>Ejemplo: 1111111111</strong></td></tr><tr><td><code>comprobante_fecha</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>La fecha del comprobante en formato dd/mm/aaaa. El día y el mes deben tener 2 dígitos.</td></tr></tbody></table>

### Emitir notas de crédito/débito anulando "por período"

A partir del 01/04/2021, AFIP habilitó la posibilidad de emitir notas de débito y/o crédito indicando un período desde/hasta en lugar del detalle de comprobantes asociados, para todo comprobante de tipo tradicional (A,B,C)

Para utilizar ésta herramienta, **no se debe enviar el bloque de "**_**comprobantes asociados"**_ **y en su lugar debe enviarse un bloque llamado **_**"comprobantes\_asociados\_periodo",**_ el cual debe tener la siguiente estructura:

```
 comprobante: {
   .... 
   ,comprobantes_asociados_periodo: {
        "fecha_desde"   :    "20/11/2020",
        "fecha_hasta"  :    "25/11/2020"  
    }
 } 
```



Estructura de los campos a enviar

| Nombre del campo | Tipo de dato               | ¿Requerido?                                  |
| ---------------- | -------------------------- | -------------------------------------------- |
| fecha\_desde     | Fecha. Formato: dd/mm/aaaa | <mark style="color:purple;">REQUERIDO</mark> |
| fecha\_hasta     | Fecha. Formato: dd/mm/aaaa | <mark style="color:purple;">REQUERIDO</mark> |
|                  |                            |                                              |

### Ejemplos JSON completos

Podes ver ejemplos de JSON completos desde aquí:

[Ejemplo Nota de crédito A](api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md#nota-de-credito-a), detallando comprobante

[Ejemplo Nota de débito A](api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md#ejemplo-de-nota-de-debito-a-asociando-periodos), asociando un periodo

[Ejemplo de Nota de crédito MiPyme](api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce.md#nota-de-credito-electronica-a-mipyme-fce)

[Ejemplo de Nota de crédito E](api-factura-electronica-afip-factura-electronica-afip-exportacion.md#ejemplo-de-nota-de-debito-e)
