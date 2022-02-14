---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  unidades de medida definidas por AFIP
---

# API Factura electrónica AFIP  | Consulta de unidades de medida para productos - AFIP

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/tablas_referencia/unidades_medida" method="post" summary="Consulta de Unidades de medida" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación.
" %}
```
{
    "error":     "N",
    "errores":  [ ""  ],
    "rta":      "OK",
    "items": 
                [  
                    {"id":"6","descripcion":"1000 kWh"},
                    {"id":"20","descripcion":"cent\u00edmetros"},
                    {"id":"27","descripcion":"cm c\u00fabicos"},
                ]
    }
```
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar

```
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6"
}
```
