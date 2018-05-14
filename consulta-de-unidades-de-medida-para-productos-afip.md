# Consulta de unidades de medida para productos - AFIP

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api/" path="v2/tablas\_referencia/unidades\_medida" %}
{% api-method-summary %}
Consulta de Unidades de medida
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación.
{% endapi-method-response-example-description %}

```
{
    "error":     "N"    "errores":                [                    ""                ]    "rta":      "OK",    "items":        [            {"id":"6","descripcion":"1000 kWh"},            {"id":"20","descripcion":"cent\u00edmetros"},            {"id":"27","descripcion":"cm c\u00fabicos"},            {"id":"48","descripcion":"curie"},            {"id":"30","descripcion":"dam c\u00fabicos"},            {"id":"9","descripcion":"docenas"}        ]}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON a enviar

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85","apikey"    :  "9991","apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6"}
```

