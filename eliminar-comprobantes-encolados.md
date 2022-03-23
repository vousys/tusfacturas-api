---
description: >-
  Utiliza la API de TusFacturasAPP, para eliminar aquellos comprobantes que se
  encuentran en cola de procesamiento
---

# Eliminar comprobantes encolados

Mediante éste método podrás eliminar aquellos comprobantes de la cola de procesamiento.

Tipo de datos: **JSON**\
Charset: **UTF-8**

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/eliminar_encolado " method="post" summary="Eliminar uno o más comprobantes en cola de procesamiento" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="external_reference" type="String" %}
Campo alfanumérico de hasta 255 caracteres.
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
    "apitoken":"XXXX",
    "apikey": XXX,
    "usertoken":"XXXX",
	"external_reference": "mi_extref" ,
	"fecha": "23/03/2022" 	 
}
 
```

### Ejemplo de respuestas posibles

Dado que podría llegar a existir +1 comprobante para una misma external\_reference (no debería), existen 3  tipos de respuesta posible.

1. Éxito
2. Éxito parcial
3. Error&#x20;

#### Éxito:

Al enviar la petición recibirás instantáneamente la siguiente respuesta:

```
{
	"error": "N",
	"errores": [],
	"procesados_cant": 1,
	"procesados": [
		"El comprobante FACTURA A 00010-00000000 se ha eliminado correctamente. "
	]
}
```

y también recibirás un webhook, para informarte de dicha eliminación:

```
{
	"creado": "18/03/2022 15:58:11",
	"evento": "eliminado",
	"recurso": "facturacion",
	"external_reference": "mi_extref",
	"intento": 1,
	"msg": [],
	"hook_id": "xxxxx"
}
```

#### Éxito parcial:

En el supuesto caso que exista +1 comprobante, para una misma external\_reference y no todas apliquen a los criterios necesarios para eliminar el comprobante:

```
{
	"error": "PARCIAL",
	"errores": [
		"El comprobante FACTURA B 00010-000000 no se ha podido eliminar."
	],
	"procesados_cant": 1,
	"procesados": [
		"El comprobante FACTURA A 00010-00000000 se ha eliminado correctamente. "
	]
}
```

#### Error:&#x20;

```
{
	"error": "S",
	"errores": [
		"No se han encontrado comprobantes."
	],
	"procesados_cant": 0,
	"procesados": []
}
```
