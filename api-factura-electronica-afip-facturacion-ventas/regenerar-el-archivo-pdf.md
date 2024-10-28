---
description: >-
  La API de facturación electrónica AFIP de TusFacturasAPP, te permite regenerar
  el archivo pdf de tu comprobante las veces que necesites.
---

# Regenerar el archivo PDF

## Regeneración de PDFs

La funcionalidad de regeneración de PDF permite recrear el comprobante con el diseño y los datos actuales que tengas configurados en la plataforma. Esto es útil si has actualizado el logo, información de cabecera u otros elementos visuales de tu documento. Puedes realizar esta operación directamente a través de este método en la API o desde la plataforma web, siguiendo la ruta: Menú > Facturación > Mis ventas. Al seleccionar el ícono correspondiente al comprobante que deseas actualizar, verás la opción de "Regenerar PDF".



<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`regenerar_pdf`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.&#x20;

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
"comprobante_pdf_url"    :  "http://www.prueba.com",
"comprobante_ticket_url": "https://www.dominio.com/url"
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
        "comprobante_pdf_url"    :  "http://www.prueba.com", 
        "comprobante_ticket_url": "https://www.dominio.com/url"
}
```

