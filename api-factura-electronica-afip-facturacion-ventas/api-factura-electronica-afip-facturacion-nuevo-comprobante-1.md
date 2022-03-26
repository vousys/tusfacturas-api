---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para emitir
  comprobantes de venta desde tu sistema actual y enviarlo a nuestra cola de
  procesamiento.
---

# Facturación asincrónica e  individual (encolada)

Una vez configurada tu cuenta y creado tu CUIT+PDV, podrás comenzar a emitir facturas electrónicas.&#x20;

Te sugerimos revisar el apartado de [¿Cómo empiezo?](../como-empiezo.md) si es la primera vez que utilizas nuestros servicios.&#x20;

## **Facturación asincrónica e individual (encolada)**

Al utilizar éste servicio, los comprobantes que emitas, quedarán en una cola de procesamiento. A medida que se van procesando, se te enviará un [webhook](../webhooks-notificaciones.md) para que puedas obtener la información generada. &#x20;

Te sugerimos leer primero:&#x20;

1. La documentación de "[Facturación](./)", para conocer cómo debe componerse el request que envíes
2. La documentación "[Webhooks (notificaciones)](../webhooks-notificaciones.md)" para conocer cómo funciona el servicio de notificaciones.
3. [FAQs sobre la cola de procesamiento](../faqs-or-cola-de-procesamiento.md)

&#x20;

### ¿Cómo funciona el modo asincrónico, de facturación individual?

![](../.gitbook/assets/image.png)



{% hint style="info" %}
### Datos a tener en cuenta:

* &#x20;**La fecha que envíes en el comprobante, determina cuándo será enviado a procesar**, por lo que puedes enviar comprobantes a la cola de procesamiento con fecha posterior a hoy.  Te sugerimos leer el apartado de "[FAQs sobre la cola de procesamiento](../faqs-or-cola-de-procesamiento.md)". __&#x20;
* El request, deben venir **con el campo número en cero (0)**.
* **Debes enviar un "external\_reference" de manera obligatoria y debería ser único**. TusFacturasAPP no realiza ésta validación, por lo que si envias +1 request con el mismo external\_reference, tendrás problemas de tu lado para procesar las respuestas.
* **Tu CUIT + PDV, debe tener una** [**dirección de webhook**](../mi-cuenta/agregar-o-modificar-puntos-de-venta-pdv.md) definida, de manera obligatoria, ya que sin ella, no se podrán enviar a procesar los lotes y serán rechazados de manera instantánea.
* **No podrás enviar comprobantes de** [**tipo E**](api-factura-electronica-afip-factura-electronica-afip-exportacion.md)  **en ésta modalidad.**
* **Al momento del envío del request, la suscripción de tu espacio de trabajo se encuentre vigente, activa y posea cupo disponible**, para emitir el comprobante.
* Si se detecta al menos un (1) error de validación de datos,  no se mandará a procesar y obtendrás la respuesta al instante, no por un webhook.
{% endhint %}



### A donde enviar el request?

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/nuevo_encola" method="post" summary="Nuevo comprobante de Venta asincrónico e individual (encolado)" %}
{% swagger-description %}
Charset: UTF-8

Tipo de dato esperado: JSON&#x20;
{% endswagger-description %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" type="object" required="false" %}
Estructura de "comprobante" según se informa en el apartado de 

["facturacion"](./)


{% endswagger-parameter %}

{% swagger-parameter in="body" name="cliente" type="object" required="false" %}
Estructura de "Cliente", según se informa en el apartado de 

["facturacion"](./)


{% endswagger-parameter %}

{% swagger-response status="200" description="" %}

{% endswagger-response %}
{% endswagger %}

### **¿Que te retornaremos ?**

#### :red\_circle: Error de validación, de los datos enviados :

En el caso de un error en la etapa de validación de los datos enviados, el request no se procesará y obtendrás la respuesta al instante. No se te notificará vía webhook.

Ejemplo :

{% code title="JSON" %}
```
{
	"error": "S",
	"errores": [
		"Este comprobante no puede emitirse en este momento, ya que tienes comprobantes pendientes en la cola de procesamiento. Para evitar problemas con la numeracion, puedes intentar crearlo nuevamente, pero enviandolo a la COLA DE PROCESAMIENTO, y sera emitido cuando se terminen de procesar los anteriores."
	],
	"error_cod": [],
	"error_details": []
}
```
{% endcode %}

#### :green\_circle: Cuando el request se ha aceptado para su procesamiento:

En caso que no se detecten errores tempranos, en la etapa de validación de los datos enviados, obtendrás la siguiente respuesta de manera instantánea y recibirás un [webhook](../webhooks-notificaciones.md)  para informarte que se ha encolado, como se explica a continuación.

Ejemplo :

```
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
	"comprobante_pdf_url": ""
}
```



## Webhooks de respuesta&#x20;

Existen 3 tipos de evento posible, para el recurso de facturación que podes recibir en ésta instancia:  "encolado", "emitido" y "error".&#x20;

Te sugerimos conocer más sobre los webhooks, en la documentación de [Webhooks (notificaciones)](../webhooks-notificaciones.md).

### :purple\_circle: Hook de "encolado"  &#x20;

|   recurso   |  evento  |
| :---------: | :------: |
| facturacion | encolado |

El hook de "encolado", te informa que el request ha sido aceptado para su procesamiento. Mientras un comprobante se encuentre dentro de la cola de procesamiento, puedes realizar las siguientes operaciones:  [Cambiar fecha del comprobante](cambiar-fecha-a-comprobante-encolado.md) o [eliminar el comprobante de la cola de procesamiento](eliminar-comprobantes-encolados.md).

&#x20;El JSON que recibirás será similar al siguiente ejemplo:

```
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

El hook de "emido", te informa que el request ha sido procesado con éxito y se ha emitido el comprobante correctamente.  Una vez recibido éste hook, podrás realizar una [consulta avanzada por external\_reference](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-external-reference),  para obtener los datos generados de éste comprobante.&#x20;

El JSON que recibirás será similar al siguiente ejemplo:&#x20;

```
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

```
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



