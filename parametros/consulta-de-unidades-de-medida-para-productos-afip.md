---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  unidades de medida definidas por AFIP
---

# Parámetros: Consulta de unidades de medida AFIP, para productos

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/tablas_referencia/unidades_medida" method="post" summary="Consulta de Unidades de medida" %}
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
{% endswagger %}

### Ejemplo del JSON a enviar

```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxx"
}
```
