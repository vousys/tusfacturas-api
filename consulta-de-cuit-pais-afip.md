---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de CUIT pais definidos por AFIP
---

# API Factura electrónica AFIP  - Consulta de CUIT Pais - AFIP

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="v2/tablas\_referencia/cuit\_pais" %}
{% api-method-summary %}
Consulta de cuit país
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
        "error":     "N",
        "errores":   [ "" ],
        "items":  [
                        {"id":"51600003015","descripcion":"AFGANISTAN - Otro tipo de Entidad"},
                        {"id":"50000003015","descripcion":"AFGANISTAN - Persona Fisica"}
                  ] 
 }
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON a enviar

```text

{ 
 "usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6" 
}
```

