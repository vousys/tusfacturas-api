---
description: >-
  Mediante éste método podrás obtener en la casilla de e-mail de los
  administradores de tu cuenta, un nuevo certificado de seguridad
---

# Solicitar certificado de enlace con AFIP

El certificado se generará para el CUIT desde el cual estas haciendo la solicitud.

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/puntos_venta/certificado" method="post" summary="Solicitar certificado" %}
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

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"xxxx",
    "apitoken":"xxxx",
    "apikey":"xx" 
}
```
{% endcode %}

