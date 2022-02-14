---
description: >-
  Mediante éste método, podrás consultar el tope especificado por AFIP, para
  ventas a consumidor final, sin requisito de detallar tipo y número de
  documento del comprador.
---

# API Factura electrónica AFIP | Consulta de tope para ventas a consumidor final

{% swagger method="post" path="/facturacion/topecf" baseUrl="https://www.tusfacturas.app/app/api/v2" summary="" %}
{% swagger-description %}
Mediante éste método, podrás consultar el tope especificado por AFIP, para ventas a consumidor final, sin requisito de detallar tipo y número de documento del comprador.
{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" required="true" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" required="true" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" required="true" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
	"error": "N",
	"errores": [],
	"monto": 26228
}
```
{% endswagger-response %}
{% endswagger %}
