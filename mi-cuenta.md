---
description: Consulta de información relacionada con tu cuenta
---

# Mi Cuenta

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api" path="/v2/micuenta/consumo" %}
{% api-method-summary %}
Consultá el consumo de tu cuenta
{% endapi-method-summary %}

{% api-method-description %}
Éste método te brindara que cantidad de comprobantes podes emitir en el mes en curso, cuantos tenés programados como abono, y cuantos te quedan disponibles.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus Credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api" path="/v2/micuenta/iva\_compras\_ventas" %}
{% api-method-summary %}
Solicitá el IVA Compras - Ventas
{% endapi-method-summary %}

{% api-method-description %}
Mediante éste método, solicitarás el envío del reporte IVA compras-ventas a una casilla de e-mail determinada. Se permite 1 casilla solamente por solicitud.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="anio" type="number" required=true %}
El año del período que se consulta.
{% endapi-method-parameter %}

{% api-method-parameter name="mes" type="number" required=true %}
El mes del período que se consulta.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
La dirección de e-mail a donde se enviará el reporte
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso  
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
La respuesta es error = S o error = N
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```
{
"error":"N",
"errores":[]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Ejemplo del JSON a enviar:

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
"usertoken" :  "5ef7asdasdadsaa1b88fcabba3f",
"apikey"    :  "13562",
"apitoken"  :  "7668aadas21321adasdiaddaa6",
"mes": 11,
"anio": 2018,
"email": "tumail@dominio.com"

}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

