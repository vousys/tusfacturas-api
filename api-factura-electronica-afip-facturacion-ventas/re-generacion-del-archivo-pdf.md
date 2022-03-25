---
description: Mediante éste método podrás regenerar el archivos pdf.
---

# Re-generación del archivo PDF

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/regenerar_pdf " method="post" summary="Regeneración de PDFs" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" required="false" %}
Un objeto compuesto de los siguientes atributos: ****&#x20;

**tipo:** Campo alfanumérico. Longitud máx: 50 caracteres, conteniendo el tipo de comprobante a consultar. Ej: FACTURA A&#x20;

**operacion :** Campo alfanumérico. Longitud máx: 1 carácter. Valores permitidos (V o C) ya sea para ventas o compras.

**punto\_venta** Campo númerico para indicar el número del punto de venta.

**numero :** Campo numérico. Longitud máx: 8. Indica el número del comprobante a consultar.


{% endswagger-parameter %}

{% swagger-response status="200" description="Regenera el PDF y te devuelve la URL del archivo" %}
```
{
"error" :  "N",
"comprobante_pdf_url"    :  "http://www.prueba.com"
}
```
{% endswagger-response %}
{% endswagger %}

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
