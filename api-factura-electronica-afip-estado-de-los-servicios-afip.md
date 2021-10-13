---
description: >-
  Mediante éste servicio podrás consultar el estado de los servicios de
  facturación AFIP, como así también el estado del servicio API.
---

# Estado de los servicios AFIP

{% hint style="info" %}
Los servicios de AFIP se caen regularmente, es importante que siempre verifiques el estado de los servicios.
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/estado_servicios/alertas" method="post" summary="Consulta de estados de los servicios" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación. 

Facturación devolverá "OK" si los servicios de la AFIP funcionan bien o devolverá un mensaje de alerta con el detalle de la incidencia
" %}
{% code title="JSON" %}
```
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
	"facturacion": "OK",
	"novedades": "24\/03\/2016 | App M\u00f3vil - Actualizaci\u00f3nYa se encuentra disponible para Iphone\/Ipad , la version 2.1 de nuestra app m\u00f3vil.  Descargala! 17\/03\/2016 | Reclamo de deudas autom\u00e1tico: Ahora podes indicar la cantidad de dias desde cuando el sistema empieza a reclamarle a tu cliente la deuda. Ingres\u00e1 a cliente y configuralo ",
}

```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar para consultar el estado de los servicios

{% code title="JSON" %}
```
{
	"usertoken": "jajajja8c8bf67c884e1405e26c03c85",
	"apikey": "9991",
	"apitoken": "kkakak208a17cdfc4e4741437baddaa6"
}
```
{% endcode %}
