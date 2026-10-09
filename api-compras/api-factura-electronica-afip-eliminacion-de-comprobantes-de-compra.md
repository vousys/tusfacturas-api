---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para
  eliminar tus comprobantes de compra.
---

# Compras: Eliminación de comprobantes

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">**`comprobante_eliminar`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request = 1 llamada`\
Los requests se cuentan individualmente por cada método que consumas [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

IMPORTANTE: Solo podrás eliminar comprobantes de compra si éstos no tienen pagos relacionados. Las compras son comprobantes solo para tu gestión interna y no impactan en ARCA.&#x20;

#### Request Body

| Name        | Type   | Description                           |
| ----------- | ------ | ------------------------------------- |
| comprobante | object | Según estructura que se detalla abajo |
| apikey      | string | Tus credenciales de acceso            |
| apitoken    | string | Tus Credenciales de acceso            |
| usertoken   | string | Tus Credenciales de acceso            |

### Ejemplo de JSON a enviar para eliminar un comprobante:

```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "C",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}
```

### Estructura de "comprobante"

| `tipo`        | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de de compra (C).<br>Valores Permitidos: <strong>C</strong><br><strong>Ejemplo: C</strong></p>                                                  |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero`      | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |

### Ejemplo del JSON de respuesta

```
{"error":"N",
"errores":[],
"rta":"El comprobante se ha eliminado."}
```

