---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de CUIT pais definidos por AFIP
---

# API Factura electrónica AFIP  | Consulta de CUIT País en AFIP

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="v2/tablas_referencia/cuit_pais" method="post" summary="Consulta de cuit país" %}
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
        "errores":   [ "" ],
        "items":  [
                        {"id":"51600003015","descripcion":"AFGANISTAN - Otro tipo de Entidad"},
                        {"id":"50000003015","descripcion":"AFGANISTAN - Persona Fisica"}
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
