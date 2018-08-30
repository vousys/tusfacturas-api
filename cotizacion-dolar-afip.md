---
description: >-
  A continuación se muestran un ejemplo de la información en JSON que debe
  recibir la API para poder  consultar con la cotización del dia según AFIP.
---

# Cotización Dólar AFIP

{% hint style="info" %}
Ésta información es actualizada a cada hora desde AFIP.
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api" path="/v2/tablas\_referencia/cotizacion" %}
{% api-method-summary %}
Obtener cotización del dólar
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="apikey" type="string" required=false %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=false %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=false %}
Tus credenciales de acceso  
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
  
En caso de existir errores, se devolverá la variable `error` con un valor "S" y la lista de errores detectados.  
En caso de exito, se retornará la variable `error`  en "N" y la cotización del momento.  
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Estructura del JSON a enviar

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
   "usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
   "apikey"    :  "9991",
   "apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6"
 }
```
{% endcode-tabs-item %}
{% endcode-tabs %}
