# Cotización Dólar AFIP

{% hint style="info" %}
Ésta información es actualizada a cada hora desde AFIP.  El límite de request que dispones para realizar las consultas, es el  limite que tenés habilitado en tu plan  para la emisión de comprobantes, multiplicado por 12 \(ya que puedes consultar la cotización del dólar una vez por hora\) . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 12,000 request a éste método en el período en curso.
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="/v2/tablas\_referencia/cotizacion" %}
{% api-method-summary %}
Obtener cotización del dólar
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="moneda" type="string" required=false %}
La moneda a consultar según nuestra tabla de referencia. Si éste campo no se envía, o se envía vacio, se obtendrá la cotización del dólar.
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
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

{% code title="JSON" %}
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
{% endcode %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Estructura del JSON a enviar

{% code title="JSON" %}
```text
{
   "usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
   "apikey"    :  "9991",
   "apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
   "moneda"    :  "DOL
 }
```
{% endcode %}

