---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para emitir
  comprobantes de venta desde tu sistema actual y enviarlo a nuestra cola de
  procesamiento.
---

# Facturación asincrónica e  individual (encolada)

TusFacturasAPP es un proveedor líder de servicios de facturación electrónica en Argentina, que permite a empresas de todos los tamaños emitir comprobantes fiscales válidos de manera rápida, segura y cumpliendo con todas las regulaciones de la AFIP.

Integra fácilmente la facturación electrónica en tu software con la API de TusFacturasAPP. Emite comprobantes fiscales válidos desde tu sistema y obtén respuestas inmediatas de la AFIP.

Una vez configurada tu cuenta y creados tus CUIT/Puntos de Venta, podrás comenzar a facturar electrónicamente sin demoras. Revisa nuestras guías "[Cómo empiezo](../como-empiezo.md)" y  "[API Facturación AFIP](./)" para conocer a fondo el servicio y los requerimientos de cada solicitud.

Comienza ya a cumplir con las regulaciones fiscales y brinda una experiencia de facturación digital eficiente a tus clientes. Solicita acceso a nuestra API de facturación electrónica.

## **Facturación asincrónica e individual (encolada)**

Al utilizar éste servicio, los comprobantes que emitas, quedarán en una cola de procesamiento. A medida que se van procesando, se te enviará un [webhook](../webhooks-notificaciones.md) para que puedas obtener la información generada. &#x20;

Te sugerimos leer primero:&#x20;

1. La documentación de "[Facturación](./)", para conocer cómo debe componerse el request que envíes
2. La documentación "[Webhooks (notificaciones)](../webhooks-notificaciones.md)" para conocer cómo funciona el servicio de notificaciones.
3. [FAQs sobre la cola de procesamiento](../faqs-or-cola-de-procesamiento.md)

&#x20;

### ¿Cómo funciona el modo asincrónico de facturación individual?

1. Tu servidor envía el request a TusFacturasAPP y éste queda en cola de procesamiento.&#x20;
2. A medida que TF va procesando, te envían un webhook con la respuesta de ese procesamiento (puede ser de éxito o error)
3. En caso que recibas una respuesta exitosa, deberás consultar el comprobante usando el método de [consulta avanzada por external\_reference](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas/consulta-avanzada-de-comprobantes-enviados#como-realizar-una-consulta-avanzada-por-external-reference)

{% hint style="info" %}
### Datos a tener en cuenta:

* &#x20;**La fecha que envíes en el comprobante, determina cuándo será enviado a procesar**, por lo que puedes enviar comprobantes a la cola de procesamiento con fecha posterior a hoy.  Te sugerimos leer el apartado de "[FAQs sobre la cola de procesamiento](../faqs-or-cola-de-procesamiento.md)".&#x20;
* El request, deben venir **con el campo número en cero (0)**.
* **Debes enviar un "external\_reference" de manera obligatoria y debería ser único**. TusFacturasAPP no realiza ésta validación, por lo que si envias +1 request con el mismo external\_reference, tendrás problemas de tu lado para procesar las respuestas.
* **Tu CUIT + PDV, debe tener una** [**dirección de webhook**](../mi-cuenta/agregar-o-modificar-puntos-de-venta-pdv.md) definida, de manera obligatoria, ya que sin ella, no se podrán enviar a procesar los requests y serán rechazados de manera instantánea.
* **No podrás enviar comprobantes de** [**tipo E**](api-factura-electronica-afip-factura-electronica-afip-exportacion.md)  **en ésta modalidad.**
* Si creas abonos, tené en cuenta que no recibirás un hook por cada vez que el abono se emita, solo con la primera emisión. (funcionalidad en desarrollo)
* **Al momento del envío del request, la suscripción de tu espacio de trabajo debe encontrarse vigente, activa y con cupo de facturación disponible** para emitir el comprobante (aunque no se emita hoy).
* Si se detecta al menos un (1) error de validación de datos,  no se mandará a procesar y obtendrás la respuesta al instante, no por un webhook.
{% endhint %}

### ¿Qué dato adicional debe tener el request para ser procesado?

Los request que se envíen de manera asincrónica deben contar con el campo de "external\_reference" presente dentro del bloque de "comprobante" , como se visualiza en éste ejemplo de código capturado  [desde aquí](./#estructura-generica-para-el-envio-de-un-comprobante).  Ej:

```
 "comprobante":{
      "external_reference":"ABC123",
      ...
}
```

### ¿Donde debo enviar los request?

#### Nuevo comprobante de Venta asincrónico e individual (encolado)

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/nuevo_encola`

Charset: UTF-8

Tipo de dato esperado: JSON&#x20;

#### Request Body

| Name        | Type   | Description                                                                        |
| ----------- | ------ | ---------------------------------------------------------------------------------- |
| usertoken   | string | Tus credenciales de acceso                                                         |
| apitoken    | string | Tus credenciales de acceso                                                         |
| apikey      | string | Tus credenciales de acceso                                                         |
| comprobante | object | Estructura de "comprobante" según se informa en el apartado de ["facturacion"](./) |
| cliente     | object | Estructura de "Cliente", según se informa en el apartado de ["facturacion"](./)    |

### **¿Que te retornaremos ?**

#### :red\_circle: ERROR: Error de validación de los datos enviados :

Si el request enviado, posee errores en la validación o formato de los campos enviados, pero  cumple con los siguientes requisitos básicos:

* Tu CUIT/PDV tiene una dirección de webhook valida
* Tu request cuenta con el campo "external\_reference"&#x20;

Recibirás la respuesta al instante y también se te notificará vía webhook.&#x20;

Ejemplo de un request, cuya external\_reference no es válida:

{% code title="JSON" %}
```json
{
	"error": "S",
	"errores": [
		"La external reference enviada, posee caracteres no validos.",
		"Error al crear al cliente . No se podra generar el comprobante. Revise los datos enviados."
	],
	"error_cod": [],
	"error_details": [
		{
			"code": "TFC-8002",
			"text": "La external reference enviada, posee caracteres no validos."
		},
		{
			"code": "TFC-6001",
			"text": "Error al crear al cliente . No se podra generar el comprobante. Revise los datos enviados."
		}
	],
	"external_reference": "1%'703"
}

```
{% endcode %}

Ejemplo del hook que recibirás:

```json
{
	"creado": "24\/05\/2022 16:58:51",
	"evento": "error",
	"recurso": "facturacion",
	"external_reference": "1%'703",
	"intento": 1,
	"msg": ["La external reference enviada, posee caracteres no validos.", "Error al crear al cliente . No se podra generar el comprobante. Revise los datos enviados."],
	"hook_id": "xxxx"
}
```

En cambio, si tu request **no cumple con los requisitos básicos** previamente mencionados, solo recibirás al instante la respuesta y no se te notificará por webhook (el comprobante no entrará en la cola de procesamiento)

```json
{
	"error": "S",
	"errores": [
		"Cuando se envia un comprobante a la cola, debes enviar una referencia externa en el campo external_reference.",
		"La external reference enviada, posee caracteres no validos.",
		"Error al crear al cliente . No se podra generar el comprobante. Revise los datos enviados."
	],
	"error_cod": [],
	"error_details": [
		{
			"code": "TFC-8002",
			"text": "Cuando se envia un comprobante a la cola, debes enviar una referencia externa en el campo external_reference."
		},
		{
			"code": "TFC-8002",
			"text": "La external reference enviada, posee caracteres no validos."
		},
		{
			"code": "TFC-6001",
			"text": "Error al crear al cliente . No se podra generar el comprobante. Revise los datos enviados."
		}
	],
	"external_reference": ""
}
```



#### :green\_circle: ACEPTADO: Cuando el request se ha aceptado para su procesamiento:

En caso que no se detecten errores tempranos, en la etapa de validación de los datos enviados, obtendrás la siguiente respuesta de manera instantánea y recibirás un [webhook](../webhooks-notificaciones.md)  para informarte que se ha encolado, como se explica a continuación.

Ejemplo :

```json
{
	"error": "N",
	"errores": [],
	"error_cod": [],
	"error_details": [],
	"external_reference": "ex_rf1",
	"requiere_fec": "NO",
	"observaciones": "",
	"tfc_generacion_tipo": 6,
	"rta": "El comprobante  se ha guardado correctamente ",
	"cae": " ",
	"vencimiento_cae": "01\/01\/2000",
	"vencimiento_pago": "21\/03\/2022",
	"comprobante_nro": "00010-00000000",
	"comprobante_tipo": "FACTURA A",
	"afip_codigo_barras": "",
	"afip_qr": "",
	"envio_x_mail": "N",
	"envio_x_mail_direcciones": "",
	"micrositios": {
			"cliente": "",
			"descarga":""
		     },
	"comprobante_pdf_url": ""
}
```



## Webhooks de respuesta&#x20;

Existen 3 tipos de eventos posibles para el recurso de facturación que podes recibir en ésta instancia:  "encolado", "emitido" y "error".&#x20;

Te sugerimos conocer más sobre los webhooks, en la documentación de [Webhooks (notificaciones)](../webhooks-notificaciones.md).

### :purple\_circle:  Hook de "encolado"  &#x20;

|   recurso   |  evento  |
| :---------: | :------: |
| facturacion | encolado |

El hook de "encolado", te informa que el request ha sido aceptado para su procesamiento. Mientras un comprobante se encuentre dentro de la cola de procesamiento, puedes realizar las siguientes operaciones:  [Cambiar fecha del comprobante](cambiar-fecha-a-comprobante-encolado.md) o [eliminar el comprobante de la cola de procesamiento](eliminar-comprobantes-encolados.md).

&#x20;El JSON que recibirás será similar al siguiente ejemplo:

```json
{
	"creado": "18/03/2022 15:58:11",
	"evento": "encolado",
	"recurso": "facturacion",
	"external_reference": "17032",
	"intento": 1,
	"msg": [],
	"hook_id": "xxxxx"
}
```

### &#x20;:green\_circle: Hook de "emitido"&#x20;

|   recurso   |  evento |
| :---------: | :-----: |
| facturacion | emitido |

El hook de "emido", te informa que el request ha sido procesado con éxito y se ha emitido el comprobante correctamente.  Una vez recibido éste hook, podrás realizar una [consulta avanzada por external\_reference](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-external-reference),  para obtener la información de éste comprobante generado.&#x20;

El JSON que recibirás será similar al siguiente ejemplo:&#x20;

```json
{
	"creado": "18/03/2022 15:58:11",
	"evento": "emitido",
	"recurso": "facturacion",
	"external_reference": "17032",
	"intento": 1,
	"msg": [],
	"hook_id": "xxx"
} 
```

### :red\_circle: Hook de "error"&#x20;

|   recurso   | evento |
| :---------: | :----: |
| facturacion |  error |

El hook de "error", te informa que el request ha sido procesado, pero se han detectado errores y no se podrá facturar. Si un comprobante se encuentra procesado con error dentro de la cola de procesamiento, puedes realizar las siguientes operaciones:  [Cambiar fecha del comprobante,](cambiar-fecha-a-comprobante-encolado.md) [re-enviar el comprobante a la cola de procesamiento](reenviar-a-procesar-comprobante-encolado-con-error.md) o [eliminar el comprobante de la cola de procesamiento](eliminar-comprobantes-encolados.md).

El JSON que recibirás será similar al siguiente ejemplo y a diferencia de los anteriores, obtendrás la lista de errores detectados, dentro del campo "msg".

```json
{
	"creado": "18/03/2022 15:58:11",
	"evento": "error",
	"recurso": "facturacion",
	"external_reference": "17032",
	"intento": 1,
	"msg": [
		" AFIP Factura electronica, informa el siguiente error: Cod. Error: #6661145.0 - AFIP rechazo la generacion del comprobante Si necesitas ayuda, contactanos en hola@tusfacturas.app", 
		" AFIP Factura electronica, informa el siguiente error: Cod. Error: #6661145.10036 - El campo FchVtoPago no puede ser anterior a la fecha del comprobante. Si necesitas ayuda, contactanos en hola@tusfacturas.app", 
		"AFIP No devolvio el CAE asociado. (Cod. Error #6661141.S1254)", 
		"AFIP No devolvio el CAE asociado. (Cod. Error #6661141.S1278)"
	],
	"hook_id": "xxx"
}  
```



