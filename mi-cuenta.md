---
description: >-
  Consulta desde la API de TusFacturas.app, la información relacionada con tu
  cuenta.
---

# Mi Cuenta - consumo

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/micuenta/consumo" method="post" summary="Consultá el consumo de tu cuenta" %}
{% swagger-description %}
Éste método te brindara que cantidad de comprobantes podes emitir en el mes en curso, cuantos tenés programados como abono, y cuantos te quedan disponibles.
{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus Credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
{% code title="JSON" %}
```
{
"error":"N",
"errores":[],
"abonos_pendientes":21,
"comprobantes_generados":12,
"comprobantes_cupo":100,
"comprobantes_disponibles": 79
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"JHJKHJHJKHJK",
    "apitoken":"HJKHJHJKHKJHK",
    "apikey":"111" 
}
```
{% endcode %}

### Ejemplo del JSON de respuesta

```
{
"error":"N",
"errores":[],
"abonos_pendientes":21,
"comprobantes_generados":12,
"comprobantes_cupo":100,
"comprobantes_disponibles": 79
}
```

##
