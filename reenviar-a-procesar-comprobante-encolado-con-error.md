---
description: >-
  Utiliza la API de TusFacturasAPP, para re-enviar a procesar aquellos
  comprobantes que se encuentran en cola de procesamiento con error
---

# Reenviar a procesar, comprobante encolado con error

{% hint style="info" %}
**ATENCIÓN!** Éste servicio comenzará a funcionar a partir del 01/04/2022
{% endhint %}

Mediante éste método podrás reenviar a procesar, un comprobante que se encuentra en cola de procesamiento con error.&#x20;

{% hint style="info" %}
Ten en cuenta que si el error que te indica es error de datos, por más que lo envies a reprocesar, no se va a emitir, ya que deberás modificarlo. En ese caso te sugerimos [eliminarlo de la cola](eliminar-comprobantes-encolados.md) y volverlo a enviar con la información correcta.
{% endhint %}



Tipo de datos: **JSON**\
Charset: **UTF-8**

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/reenviar_encolado " method="post" summary="Envía nuevamente a procesar, un comprobante que se encuentra en cola de procesamiento con error. " %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="external_reference" type="String" %}
Campo alfanumérico de hasta 255 caracteres.
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
    "external_reference": "mi_ext_rf"  
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

y también recibirás un webhook, para informarte que el comprobante se ha enviado a la cola de procesamiento:

```
{
	"creado": "18/03/2022 15:58:11",
	"evento": "encolado",
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
