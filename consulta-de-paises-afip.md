---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de paises definidos por AFIP
---

# API Factura electrónica AFIP  | Consulta de Países en AFIP

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="v2/tablas_referencia/paises" method="post" summary="Consulta de paises " %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación.

" %}
{% code title="JSON" %}
```
 {
	"error": "N",
	"errores": [""],
	"items": [{
		"id": "250",
		"descripcion": "AAE Tierra del Fuego - ARGENTINA"
	}, {
		"id": "301",
		"descripcion": "AFGANISTAN"
	}]
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

### Estructura del JSON a enviar

{% code title="JSON" %}
```
{
	"usertoken": "jajajja8c8bf67c884e1405e26c03c85",
	"apikey": "9991",
	"apitoken": "kkakak208a17cdfc4e4741437baddaa6"
}

```
{% endcode %}
