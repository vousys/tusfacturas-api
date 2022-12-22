---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de CUIT pais definidos por AFIP
---

# Parámetros:  Consulta de los CUIT País en AFIP

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="v2/tablas_referencia/cuit_pais" method="post" summary="Consulta de cuit país" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de no existir errores, se devolverá la variable error con un valor " %}
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
 "usertoken" :  "xxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxxx" 
}
```
