---
description: >-
  Utiliza la API de TusFacturasAPP, para cambiar la fecha de aquellos
  comprobantes que se encuentran en cola de procesamiento
---

# Cambiar fecha a comprobante encolado

Mediante éste método podrás cambiar la fecha de un  comprobante que se encuentre en cola de procesamiento.&#x20;

Ten en cuenta, que la fecha del comprobante, determina la fecha en que éste se emitirá.



Tipo de datos: **JSON**\
Charset: **UTF-8**

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/cambiar_fecha_encolado " method="post" summary="Cambiar la fecha de uno o más comprobantes en cola de procesamiento" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="external_reference" type="String" %}
Campo alfanumérico de hasta 255 caracteres.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vencimiento" type="String" %}
Fecha de vencimiento del pago de dicho comprobante. Formato esperado: dd/mm/aaaa
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fecha" type="string" %}
Fecha del comprobante. Formato esperado: dd/mm/aaaa
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus Credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus Credenciales de acceso.
{% endswagger-parameter %}

{% swagger-response status="200" description=" " %}

{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar:

```
{
    "apitoken":"xxxx",
    "apikey": "xxx",
    "usertoken":"xxxx",
    "external_reference": "mi_ext_rf" ,
    "fecha": "25/03/2022",
    "vencimiento": "28/03/2022"
	 
}
 
```

### Ejemplo de respuestas posibles

En caso de existir +1 comprobante para una misma external\_reference (no debería), se tomará al primero encontrado.&#x20;

#### Éxito:

Al enviar la petición, recibirás instantáneamente la siguiente respuesta:

```
{
	"error": "N",
	"errores": []
}
```

y también recibirás un webhook, para informarte de dicha eliminación:

```
{
	"creado": "18/03/2022 15:58:11",
	"evento": "cambio_fecha",
	"recurso": "facturacion",
	"external_reference": "mi_extref",
	"intento": 1,
	"msg": [],
	"hook_id": "xxxxx"
}
```

#### Error:&#x20;

```
{
	"error": "S",
	"errores": [
		"No se han encontrado comprobantes."
	]
}
```
