---
description: >-
  Mediante éste método podrás consultar si los servicios de AFIP se encuentran
  funcionando correctamente y/o si nuestra plataforma tiene que notificarte
  algún evento.
---

# Estado de los servicios AFIP

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api/" path="v2/estado\_servicios/alertas" %}
{% api-method-summary %}
Consulta de estados de los servicios
{% endapi-method-summary %}

{% api-method-description %}

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
Tus credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación.   
  
Facturación devolverá "OK" si los servicios de la AFIP funcionan bien o devolverá un mensaje de alerta con el detalle de la incidencia  
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
	"facturacion": "OK",
	"novedades": "24\/03\/2016 | App M\u00f3vil - Actualizaci\u00f3nYa se encuentra disponible para Iphone\/Ipad , la version 2.1 de nuestra app m\u00f3vil.  Descargala! 17\/03\/2016 | Reclamo de deudas autom\u00e1tico: Ahora podes indicar la cantidad de dias desde cuando el sistema empieza a reclamarle a tu cliente la deuda. Ingres\u00e1 a cliente y configuralo ",
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON a enviar para consultar el estado de los servicios

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
	"usertoken": "jajajja8c8bf67c884e1405e26c03c85",
	"apikey": "9991",
	"apitoken": "kkakak208a17cdfc4e4741437baddaa6"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

