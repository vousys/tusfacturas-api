---
description: >-
  Utiliza la API de TusFacturasAPP, para cambiar la fecha de aquellos
  comprobantes que se encuentran en cola de procesamiento
---

# Cambiar fecha a comprobante encolado

Mediante éste método podrás cambiar la fecha de un  comprobante que se encuentre en cola de procesamiento.&#x20;

Ten en cuenta, que la fecha del comprobante, determina la fecha en que éste se emitirá y siempre se emiten de la cola, aquellos comprobantes que tengan fecha menor o igual a hoy.



Tipo de datos: **JSON**\
Charset: **UTF-8**

## Cambiar la fecha de uno o más comprobantes en cola de procesamiento

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/cambiar_fecha_encolado`&#x20;

#### Request Body

| Name                | Type   | Description                                                                      |
| ------------------- | ------ | -------------------------------------------------------------------------------- |
| apikey              | string | Tus credenciales de acceso.                                                      |
| apitoken            | string | Tus Credenciales de acceso.                                                      |
| usertoken           | string | Tus Credenciales de acceso.                                                      |
| fecha               | string | Fecha del comprobante. Formato esperado: dd/mm/aaaa                              |
| external\_reference | String | Campo alfanumérico de hasta 255 caracteres.                                      |
| vencimiento         | String | Fecha de vencimiento del pago de dicho comprobante. Formato esperado: dd/mm/aaaa |

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
