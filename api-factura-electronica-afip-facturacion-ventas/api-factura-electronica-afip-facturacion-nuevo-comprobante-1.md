---
description: >-
  TusFacturasAPP: La solución SaaS líder para automatizar tu facturación
  electrónica. Integración API AFIP/ARCA asincrónica.
icon: a
---

# Facturación asincrónica e  individual

### ⚡ ¿Qué es la API de facturación individual y asincrónica? <a href="#que-es-la-api-de-facturacion-individual-e-instantanea" id="que-es-la-api-de-facturacion-individual-e-instantanea"></a>

La **API de ARCA para facturación electrónica individual y asincrónica de TusFacturasAPP** te permite **emitir comprobantes fiscales válidos ante ARCA**. Es ideal para grandes volúmenes de facturación o cuándo el funcionamiento de tu plataforma no dependa del estado en tiempo real  de los servicios de ARCA. Integra fácil la facturación electrónica de AFIP/ARCA a tu sistema, cumpliendo con las normativas fiscales vigentes en Argentina.

<figure><img src="../.gitbook/assets/157.webp" alt="SDK AFIP. TusFacturasAPP API Factura Electronica AFIP. AFIP WS"><figcaption></figcaption></figure>

### ¿Cómo empiezo?

Te sugerimos revisar la guia de [¿Cómo empiezo?](../como-empiezo/) . Una vez configurada tu cuenta y creado tu CUIT+Punto de venta (PDV) en [TusFacturasAPP](https://www.tusfacturas.app), podrás comenzar a emitir facturas electrónicas AFIP Argentina válidas.&#x20;

### 🛠 ¿Cómo funciona la modalidad Asincrónica de Facturación ARCA/AFIP?

{% stepper %}
{% step %}
### Envias un request a TusFacturasAPP

Tu plataforma debe enviar el [`request`](referencia-api-afip-arca.md) del comprobante a TusFacturasAPP sin incluir el número de factura. Si es válido, el comprobante se añadirá a una cola de procesamiento.
{% endstep %}

{% step %}
### Se genera la factura, nota de débito o nota de crédito

Si el comprobante se pudo facturar, generamos el PDF y le enviamos a tu cliente un email para que descargue el comprobante.
{% endstep %}

{% step %}
### TusFacturasAPP te envia un hook

A medida que se procesan las ventas, TusFacturasAPP te envía [webhooks](webhooks-notificaciones.md) con diferentes eventos:\
\- encolado\
\- emitido\
\- error

Una vez recibido el hook, debes consultar la información del comprobante con una [consulta avanzada por external\_reference](../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md).
{% endstep %}
{% endstepper %}

### ⚠️ Consideraciones clave

* **La fecha que envíes en el comprobante, determina cuándo será enviado a procesar**, por lo que puedes enviar comprobantes a la cola de procesamiento con fecha posterior a hoy.  Te sugerimos leer el apartado de "[FAQs sobre la cola de procesamiento](../faqs-or-ventas-asincronicas.md)".&#x20;
* El **campo external\_reference es obligatorio** y debe ser único, sin embargo TusFacturasAPP no realiza ese control.
* **El número del comprobante debe enviarse en 0**, ya que será determinado al momento de emitirse.
* **Tu punto de venta debe tener una URL de webhook configurada**. Ésto se realiza desde nuestra plataforma web, accediendo a Menú > Mi espacio de trabajo > Puntos de venta.
* En la modalidad asincrónica no se permiten comprobantes tipo E.
* Para que tus comprobantes se emitan, **la suscripción de tu espacio de trabajo debe encontrarse vigente, activa y con cupo de facturación disponible** para emitir el comprobante (aunque no se emita hoy).
* Los errores de validación de datos bloquean el envío a la cola y generan una respuesta inmediata (no por webhook).

### ⏱ Tiempos de procesamiento

Los tiempos varían según:\
\- Volumen de ventas programadas\
\- Estado de los servicios de facturación de ARCA\
\- Tipo de comprobante a emitir

#### Capacidades máximas:

* Hasta 100.000 comprobantes A por día, por punto de venta.
* Hasta 150.000 comprobantes B por día, por punto de venta.
* Hasta   14.000 de otros tipos por día, por punto de venta.

Para acelerar la facturación podrías distribuir la carga de facturación en múltiples puntos de venta. Sin embargo, no podemos garantizar que todo el volumen se emita en un solo día, por lo que recomendamos enviar la facturación con antelación para evitar inconvenientes.

### 📄 ¿Qué dato no debe faltar  en un request asincrónico?

El bloque "comprobante" debe incluir el campo "external\_reference". Ejemplo:

```
 "comprobante":{
      "external_reference":"ABC123",
      ...
}
```

### 🚀 ¿Cómo crear una venta asincrónica? <a href="#como-crear-una-venta-instantanea" id="como-crear-una-venta-instantanea"></a>

Consultá nuestra [guía completa 👉 **“Referencia API AFIP ARCA”**](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca), donde encontrarás:

* Especificaciones técnicas
* Campos requeridos para armar el request
* [Ejemplos de código](https://developers.tusfacturas.app/web-services-afip-api-arca) listos para usar
* Buenas prácticas de integración y manejo de errores

> Con nuestra documentación clara y ejemplos reales, **la integración de la facturación electrónica en tu software será rápida, sencilla y confiable**.

### 📌 Endpoint para ventas individuales y asincrónicas

{% hint style="info" %}
<mark style="color:green;">`POST`</mark>&#x20;

`https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">**`nuevo_encola`**</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.
{% endhint %}

Charset: UTF-8  Formato: JSON&#x20;

#### Body

| Name        | Type   | Description                                                                        |
| ----------- | ------ | ---------------------------------------------------------------------------------- |
| usertoken   | string | Tus credenciales de acceso                                                         |
| apitoken    | string | Tus credenciales de acceso                                                         |
| apikey      | string | Tus credenciales de acceso                                                         |
| comprobante | object | Estructura de "comprobante" según se informa en el apartado de ["facturacion"](./) |
| cliente     | object | Estructura de "Cliente", según se informa en el apartado de ["facturacion"](./)    |



### ✅ Respuestas posibles

#### :red\_circle: ERROR  de válidación -  Respuesta: instántanea

Si el request que enviaste posee errores de formato de los campos enviados, pero  cumple con los siguientes requisitos básicos:

* Tu punto de venta tiene una dirección de webhook valida
* Tu request cuenta con el campo "external\_reference"&#x20;

Ese comprobante sera rechazado inmediatamente y recibirás la respuesta junto con el webhook de error.&#x20;

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



#### :green\_circle: ACEPTADO: Cuando el request se ha aceptado para su procesamiento

Una vez que tu solicitud pase la validación inicial, obtendrás una respuesta instantánea del sistema. Adicionalmente, para informarte que la operación ha sido encolada, se enviará un [**webhook**](webhooks-notificaciones.md), cuyo funcionamiento se explica a continuación.

Ejemplo de la respuesta instantánea :

```json
{
	"error": "N",
	"errores": [],
	"error_cod": [],
	"error_details": [],
	"external_reference": "ex_rf1",
	"requiere_fec": "NO",
	"observaciones": "",
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



### 📬 Webhooks de respuesta de la API ARCA/AFIP

Existen 3 tipos de eventos posibles para el recurso de facturación que podes recibir en ésta instancia:  "encolado", "emitido" y "error".&#x20;

Conoce más sobre los [webhooks](webhooks-notificaciones.md).

### :purple\_circle:  Hook: "encolado"  &#x20;

|   recurso   |  evento  |
| :---------: | :------: |
| facturacion | encolado |

El hook de "encolado", te informa que el request ha sido aceptado para su procesamiento. Mientras un comprobante se encuentre dentro de la cola de procesamiento, podes realizar las siguientes operaciones:  [Cambiar fecha del comprobante](../web-services-afip-api-arca/cambiar-fecha-a-comprobante-encolado.md) o [eliminar el comprobante de la cola de procesamiento](../web-services-afip-api-arca/eliminar-comprobantes-encolados.md).

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

### &#x20;:green\_circle: Hook: "emitido"&#x20;

|   recurso   |  evento |
| :---------: | :-----: |
| facturacion | emitido |

El hook de "emitido"  te informa que el request ha sido procesado con éxito y se ha emitido el comprobante correctamente.  Una vez recibido éste hook, deberás realizar una [consulta avanzada por external\_reference](consulta-avanzada.md#como-realizar-una-consulta-avanzada-por-external-reference),  para obtener la información de éste comprobante.&#x20;

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

### 🔴 Hook: "error"

|   recurso   | evento |
| :---------: | :----: |
| facturacion |  error |

El hook de "error", te informa que el request ha sido procesado, pero se han detectado errores y no se podrá facturar. Si un comprobante se encuentra procesado con error dentro de la cola de procesamiento, puedes realizar las siguientes operaciones:  [Cambiar fecha del comprobante,](../web-services-afip-api-arca/cambiar-fecha-a-comprobante-encolado.md) [re-enviar el comprobante a la cola de procesamiento](../web-services-afip-api-arca/reenvio-de-comprobantes-encolados-con-error.md) o [eliminar el comprobante de la cola de procesamiento](../web-services-afip-api-arca/eliminar-comprobantes-encolados.md).

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



### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

***

TusFacturasAPP es una solución SaaS líder en facturación electrónica en Argentina, diseñada para facilitar a empresas y desarrolladores la integración directa con los webservices de facturación de ARCA (ex AFIP) mediante una API robusta, segura y fácil de implementar.
