---
description: >-
  Utiliza la API de TusFacturasAPP, para re-enviar a procesar aquellos
  comprobantes que se encuentran en cola de procesamiento con error
---

# Re-enviar a procesar ventas AFIP asincrónicas con error

Mediante éste método podrás reenviar a procesar, un comprobante que se encuentra en cola de procesamiento con error.&#x20;

{% hint style="info" %}
Ten en cuenta que si el error que te indica es error de datos, por más que lo envies a reprocesar, no se va a emitir, ya que deberás modificarlo. En ese caso te sugerimos [eliminarlo de la cola](eliminar-comprobantes-encolados.md) y volverlo a enviar con la información correcta.
{% endhint %}



Tipo de datos: **JSON**\
Charset: **UTF-8**

## Envía nuevamente a procesar, un comprobante que se encuentra en cola de procesamiento con error.&#x20;

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`reenviar_encolado`</mark>&#x20;

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

| Name                | Type   | Description                                 |
| ------------------- | ------ | ------------------------------------------- |
| apikey              | string | Tus credenciales de acceso.                 |
| apitoken            | string | Tus Credenciales de acceso.                 |
| usertoken           | string | Tus Credenciales de acceso.                 |
| external\_reference | String | Campo alfanumérico de hasta 255 caracteres. |

{% tabs %}
{% tab title="200  " %}

{% endtab %}
{% endtabs %}

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
