---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de paises definidos por AFIP
---

# Parámetros: Consulta de Países en AFIP

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/tablas_referencia/paises" method="post" summary="Consulta de paises " %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}
{% endswagger %}

### Estructura del JSON a enviar

{% code title="JSON" %}
```
{
	"usertoken": "xxxx",
	"apikey": "xxx",
	"apitoken": "xxxx"
}
```
{% endcode %}
