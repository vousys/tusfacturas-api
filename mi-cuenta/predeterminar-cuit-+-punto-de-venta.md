---
description: >-
  Mediante éste método, podrás marcar como predeterminado el punto de venta,
  desde el cual estas realizando la solicitud.
---

# Predeterminar CUIT + Punto de venta



{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/puntos_venta/predeterminar" method="post" summary="Predeterminar CUIT + Punto de venta" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso

\\
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
	"error": "N",
	"errores": [] 
}
```
{% endswagger-response %}
{% endswagger %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"xxxx",
    "apitoken":"xxxx",
    "apikey":"xxxx" 
}
```
{% endcode %}

##
