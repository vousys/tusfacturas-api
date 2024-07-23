---
description: >-
  La API de facturación electrónica AFIP de TusFacturasAPP, te permite regenerar
  el archivo pdf de tu comprobante las veces que necesites.
---

# Re-generación del archivo PDF

## Regeneración de PDFs

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`regenerar_pdf`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción&#x20;

#### Request Body

| Name        | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| usertoken   | string | tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| apitoken    | string | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| apikey      | string | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| comprobante | String | <p>Un objeto compuesto de los siguientes atributos: </p><p><strong>tipo:</strong> Campo alfanumérico. Longitud máx: 50 caracteres, conteniendo el tipo de comprobante a consultar. Ej: FACTURA A </p><p><strong>operacion :</strong> Campo alfanumérico. Longitud máx: 1 carácter. Valores permitidos (V o C) ya sea para ventas o compras.</p><p><strong>punto_venta</strong> Campo númerico para indicar el número del punto de venta.</p><p><strong>numero :</strong> Campo numérico. Longitud máx: 8. Indica el número del comprobante a consultar.</p><p></p> |

{% tabs %}
{% tab title="200 Regenera el PDF y te devuelve la URL del archivo" %}
```
{
"error" :  "N",
"comprobante_pdf_url"    :  "http://www.prueba.com"
}
```
{% endtab %}
{% endtabs %}

### Ejemplo del JSON a enviar para re-generar el pdf

{% code title="JSON" %}
```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}

```
{% endcode %}

### Ejemplo del JSON de respuesta:

```
{
        "error" :  "N",
        "comprobante_pdf_url"    :  "http://www.prueba.com"
}
```

##
