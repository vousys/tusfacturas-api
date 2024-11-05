---
description: >-
  Utiliza la API de TusFacturasAPP, para eliminar aquellos comprobantes que se
  encuentran en cola de procesamiento
---

# Eliminar comprobantes encolados

Mediante éste método podrás eliminar aquellos comprobantes de la cola de procesamiento.

Tipo de datos: **JSON**\
Charset: **UTF-8**

## Eliminar uno o más comprobantes en cola de procesamiento

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`eliminar_encolado`</mark>&#x20;

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

| Name                | Type   | Description                                         |
| ------------------- | ------ | --------------------------------------------------- |
| apikey              | string | Tus credenciales de acceso.                         |
| apitoken            | string | Tus Credenciales de acceso.                         |
| usertoken           | string | Tus Credenciales de acceso.                         |
| fecha               | string | Fecha del comprobante. Formato esperado: dd/mm/aaaa |
| external\_reference | String | Campo alfanumérico de hasta 255 caracteres.         |

{% tabs %}
{% tab title="200  " %}

{% endtab %}
{% endtabs %}

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

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
