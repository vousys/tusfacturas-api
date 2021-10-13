---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de incoterms  .
---

# API Factura electrónica AFIP  - Consulta de Incoterms

{% swagger baseUrl=" https://www.tusfacturas.app/app/api/" path="v2/tablas_referencia/incoterms" method="post" summary="Consulta de Incoterms" %}
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

{% swagger-response status="200" description="En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación." %}
```
{
    "error":     "N",
    "errores":   
                 [  ""   ],    
     "items":       
              [ 
                       {"id":"EXW","descripcion":"EXW - Vigente del 20100101 a hoy"},
                       {"id":"FCA","descripcion":"FCA - Vigente del 20100101 a hoy"}

              ]
}
```
{% endswagger-response %}
{% endswagger %}

### Ejemplo de JSON a enviar

```
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6"
}
```
