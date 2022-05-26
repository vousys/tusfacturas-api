---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  diferentes cotizaciones de monedas brindadas por AFIP.
---

# Consultar las cotizaciones AFIP

{% hint style="info" %}
Ten en cuenta que para la moneda "dólar": AFIP trabaja con la cotización oficial del Banco de la Nación Argentina, correspondiente al DOLAR DIVISAS y la cotización es actualizada a cada hora.
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/tablas_referencia/cotizacion" method="post" summary="Obtener cotización desde AFIP" %}
{% swagger-description %}
Puedes obtener la cotización de las diferentes monedas que tenemos publicadas en nuestra

**tabla de referencia de monedas**

. La cotización es obtenida desde AFIP.
{% endswagger-description %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="moneda" type="string" required="false" %}
La moneda a consultar, según nuestra 

[tabla de referencia de monedas](../parametros/tablas-de-referencia.md#monedas)

. En caso que no envies éste dato, obtendrás la cotización del dolar.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fecha" type="string" required="false" %}
Si indicas la fecha en formato dd/mm/aaaa, te mostraremos la ultima cotización encontrada en AFIP para ese día, según los datos que hemos almacenado. Ten en cuenta que no podrás consultar mas de 2 meses atras.


{% endswagger-parameter %}
{% endswagger %}

### Estructura del JSON a enviar

{% code title="JSON" %}
```
{
   "usertoken" :  "xxxx",
   "apikey"    :  "xxxx",
   "apitoken"  :  "xxxx",
   "moneda"    :  "012",
   "fecha"     :  "02/03/2020"
 }
```
{% endcode %}

### Ejemplo de un JSON de respuesta exitosa

```
 {
        "error":     "N",
        "errores":
                    [
                        ""
                    ],
        "cotizacion": "15.10"
    }
```
