---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  diferentes cotizaciones brindadas por AFIP.
---

# Consultar las cotizaciones AFIP

{% hint style="info" %}
Ésta información es actualizada a cada hora desde AFIP. El límite de request que dispones para realizar las consultas, es el limite que tenés habilitado en tu plan para la emisión de comprobantes, multiplicado por 12 (ya que puedes consultar la cotización del dólar una vez por hora) . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 12,000 request a éste método en el período en curso.
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
La moneda a consultar, según nuestra tabla de referencia de monedas. En caso que no envies éste dato, obtendrás la cotización del dolar.
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
