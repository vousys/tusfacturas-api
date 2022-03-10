# Solicitar reporte IVA compras-ventas

Mediante éste método, solicitarás el envío del reporte IVA compras-ventas a una casilla de e-mail determinada. Se permite 1 casilla solamente por solicitud.

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/micuenta/iva_compras_ventas" method="post" summary="Solicitá el IVA Compras - Ventas" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="anio" type="number" required="false" %}
El año del período que se consulta.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mes" type="number" required="false" %}
El mes del período que se consulta.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" required="false" %}
La dirección de e-mail a donde se enviará el reporte
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="La respuesta es error = S o error = N" %}
{% code title="JSON" %}
```
{
"error":"N",
"errores":[]
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
"usertoken" :  "5ef7asdasdadsaa1b88fcabba3f",
"apikey"    :  "13562",
"apitoken"  :  "7668aadas21321adasdiaddaa6",
"mes": 11,
"anio": 2018,
"email": "tumail@dominio.com"

}
```
{% endcode %}

### Ejemplo del JSON de respuesta

```
{
"error":"N",
"errores":[]
}
```
