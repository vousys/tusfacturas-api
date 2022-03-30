---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para enviar a
  procesar lotes y obtener una respuesta asincrónica de su procesamiento,
  acelerando los tiempos de envío.
---

# Facturación asincrónica por Lotes (encolada)

Una vez configurada tu cuenta y creado tu CUIT+PDV, podrás comenzar a emitir facturas electrónicas. Te sugerimos revisar el apartado de [¿Cómo empiezo?](../como-empiezo.md) si es la primera vez que utilizas nuestros servicios

## ¿Cómo funciona el modo asincrónico, de facturación por lote?

![](../.gitbook/assets/image.png)

## ¿Qué puedo facturar por lote?

Podes enviar a facturar comprobantes de tipo A,B,C, M y comprobantes de tipo Factura de crédito electrónica MiPyme; ya sean facturas, notas de crédito, notas de débito y hasta facturas-recibos. **No podrás enviar comprobantes de tipo E  en ésta modalidad.**

&#x20;¿No sabes qué [tipo de comprobante debes emitir](../que-tipos-de-comprobante-debo-puedo-emitir.md)? Consultalo [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md)

Tenés alguna duda del servicio? checkea las [API FAQs](../faqs-or-preguntas-frecuentes.md), y si no encontrás lo que buscabas, contactanos por los canales de atención que tenemos disponibles en la plataforma web [www.tusfacturas.app](https://www.tusfacturas.app)

## **Facturación asincrónica por Lote**

Al utilizar éste servicio, los comprobantes que emitas, quedarán en una cola de procesamiento. A medida que se van procesando, se te enviará un [webhook](../webhooks-notificaciones.md) para que puedas obtener la información generada. &#x20;



Te sugerimos leer primero:&#x20;

1. La documentación de "[Facturación](./)", para conocer cómo debe componerse el request que envíes
2. La documentación "[Webhooks (notificaciones)](../webhooks-notificaciones.md)" para conocer cómo funciona el servicio de notificaciones.
3. [FAQs sobre la cola de procesamiento](../faqs-or-cola-de-procesamiento.md)

#### A donde debes enviar el request?

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/facturacion/lotes_encola" method="post" summary="Facturación por Lotes asincrónica (encolada). Max: 100 requests por lote." %}
{% swagger-description %}


Charset: UTF-8

Formato esperado: JSON
{% endswagger-description %}

{% swagger-parameter in="body" name="requests" type="array" required="false" %}
Según estructura de de cada item (detallado abajo).
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
{% code title="JSON" %}
```
{
    "error": "N",
    "errores": [],
    "response": [{
        "error": "N",
        "errores": [],
        "cae": "68466696512853 ",
        "comprobante_nro": "00003-00000074",
        "cae_vencimiento": "26\/11\/2018",
        "observaciones": "AFIP genero el comprobante pero lo ha marcado como observado por los siguientes motivos: Observacion: Factura individual, DocTipo: 80, DocNro 22222222222 no se encuentra inscripto en condicion ACTIVA en el impuesto (IVA). [ codigo: 10063 ]. Dichas observaciones no requieren accion de su parte.",
        "envio_x_mail": "N",
        "envio_x_mail_direcciones": "",
        "rta": "El comprobante FACTURA A 00003-00000074 (XXXXXX) se ha guardado correctamente ",
        "vencimiento_cae": "26\/11\/2018",
        "vencimiento_pago": "16\/11\/2018",
        "comprobante_tipo": "FACTURA A",
        "afip_codigo_barras": "111111111110010000368466696512853201811262 ",
        "comprobante_pdf_url": "https:\/\/www.dominio.com\/00000074.pdf"
    }, {
        "error": "N",
        "errores": [],
        "cae": "68466696512866 ",
        "comprobante_nro": "00003-00000075",
        "cae_vencimiento": "26\/11\/2018",
        "observaciones": "AFIP genero el comprobante pero lo ha marcado como observado por los siguientes motivos: Observacion: Factura individual, DocTipo: 80, DocNro 22222222222 no se encuentra inscripto en condicion ACTIVA en el impuesto (IVA). [ codigo: 10063 ]. Dichas observaciones no requieren accion de su parte.",
        "envio_x_mail": "N",
        "envio_x_mail_direcciones": "",
        "rta": "El comprobante FACTURA A 00003-00000075 (XXXXXX) se ha guardado correctamente ",
        "vencimiento_cae": "26\/11\/2018",
        "vencimiento_pago": "16\/11\/2018",
        "comprobante_tipo": "FACTURA A",
        "afip_codigo_barras": "111111111110010000368466696512866201811266 ",
        "comprobante_pdf_url": "https:\/\/www.dominio.com\/00000075.pdf"
    }]
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

#### Estructura del bloque: "requests"

"requests debe ser un array, que contiene cada uno de los comprobantes a emitir, según se define en la documentación de "[Facturación](./)".

{% hint style="info" %}
### Datos a tener en cuenta:

* **La cantidad máxima de requests por lote es de 100 comprobantes**, pero debes tener en cuenta que por cuestiones de seguridad, nuestra plataforma funciona limitando su tiempo de procesamiento y  puedes llegar a obtener una respuesta de timeout (524). En caso de recibir un 524, los requests que enviaste, seguirán siendo procesados en background, y recibirás un hook con la respuesta de éxito o error, de su encolamiento. &#x20;
* Puedes enviar en un mismo lote, comprobantes de **diferente tipo de comprobante**.   Ej: Puedes enviar en el mismo lote Facturas A Y FACTURAS  B.
* **La fecha que envíes en cada comprobante determina cuándo será enviado a procesar**, por lo que puedes enviar comprobantes a la cola de procesamiento con fecha posterior a hoy. __&#x20;
* Los request deben venir **con el campo número en cero (0)**.
* **Debes enviar un "external\_reference" de manera obligatoria y debería ser único**. TusFacturasAPP no realiza ésta validación, por lo que si envias +1 request con el mismo external\_reference, tendrás problemas de tu lado para procesar las respuestas.
* **Tu CUIT + PDV, debe tener una** [**dirección de webhook**](../mi-cuenta/agregar-o-modificar-puntos-de-venta-pdv.md) definida, de manera obligatoria, ya que sin ella, no se podrán enviar a procesar los lotes y serán rechazados de manera instantánea.
* **No podrás enviar comprobantes de** [**tipo E**](api-factura-electronica-afip-factura-electronica-afip-exportacion.md)  **en ésta modalidad.**
* **Al momento del envío del lote, la suscripción de tu espacio de trabajo se encuentra vigente, activa y posee cupo disponible**, para emitir la cantidad de comprobante que estás enviando en el lote.
* Si se detecta al menos un (1) error de validación de datos, el lote no se mandará a procesar y obtendrás la respuesta al instante, no por un webhook.


{% endhint %}

La estructura de cada "request" debe ser acorde a los siguientes tipos de comprobante a generar ([comprobantes de tipo A](api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md), [comprobantes de tipo B](api-factura-electronica-afip-factura-nota-de-debito-b-nota-de-credito-bb.md), [comprobantes de tipo C](api-factura-electronica-afip-factura-c-nota-de-debito-c-nota-de-credito-c.md)[ ](api-factura-electronica-afip-factura-electronica-afip-exportacion.md), [Comprobantes de tipo Factura de crédito electrónica MiPyme](api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce.md)) .

#### Ejemplo de JSON a enviar

{% code title="JSON" %}
```
{
	"apitoken": "xxxx",
	"apikey": "xxxx",
	"usertoken": "xxxxx",
	"requests": [{
			"apitoken": "xxxxx",
			"apikey": "xxxxx",
			"usertoken": "xxxxx",
			"cliente": {
				"documento_tipo": "CUIT",
				"condicion_iva": "M",
				"domicilio": "Av Sta Fe 23132",
				"condicion_pago": "211",
				"documento_nro": "3071229384",
				"razon_social": "VOUSYS",
				"provincia": "2",
				"email": "email@dominio.com",
				"envia_por_mail": "N"
			},
			"comprobante": {
				"external_reference": "AAAA",
				"rubro": "Sevicios web",
				"percepciones_iva": 0,
				"tipo": "FACTURA B",
				"numero": 1,
				"percepciones_iibb": 0,
				"bonificacion": 0,
				"operacion": "V",
				"detalle": [{
					"cantidad": 1,
					"producto": {
						"descripcion": "Hosting pagina web ",
						"codigo": 37,
						"lista_precios": "standard",
						"leyenda": "",
						"unidad_bulto": 1,
						"alicuota": 21,
						"precio_unitario_sin_iva": 114.88
					}
				}],
				"fecha": "28/03/2022",
				"rubro_grupo_contable": "Sevicios",
				"total": 139.0,
				"cotizacion": 1,
				"moneda": "PES",
				"punto_venta": 3,
				"percepciones_iibb": "0",
				"percepciones_iibb_base": "0",
				"percepciones_iibb_alicuota": "0",
				"percepciones_iva": "0",
				"percepciones_iva_base": "0",
				"percepciones_iva_alicuota": "0",
				"exentos": "0",
				"impuestos_internos": "0",
				"impuestos_internos_base": "0",
				"impuestos_internos_alicuota": "0"
			}
		},
		{
			"apitoken": "xxxxx",
			"apikey": "xxxxx",
			"usertoken": "xxxxx",

			"cliente": {
				"documento_tipo": "CUIT",
				"condicion_iva": "RI",
				"domicilio": "XXX",
				"condicion_pago": "211",
				"documento_nro": "30712252430",
				"razon_social": "VYAR SRL",
				"provincia": "2",
				"email": "email@dominio.com",
				"envia_por_mail": "N"
			},
			"comprobante": {
				"rubro": "Sevicios web",
				"percepciones_iva": 0,
				"tipo": "FACTURA A",
				"external_reference": "ABC124",
				"numero": 0,
				"percepciones_iibb": 0,
				"bonificacion": 0,
				"operacion": "V",
				"detalle": [{
					"cantidad": 1,
					"producto": {
						"descripcion": "Hosting pagina web ",
						"codigo": 37,
						"lista_precios": "standard",
						"leyenda": "",
						"unidad_bulto": 1,
						"alicuota": 21,
						"precio_unitario_sin_iva": 114.88
					}
				}],
				"fecha": "28/03/2022",
				"rubro_grupo_contable": "Sevicios",
				"total": 139.0,
				"cotizacion": 1,
				"moneda": "PES",
				"punto_venta": 3,
				"percepciones_iibb": "0",
				"percepciones_iibb_base": "0",
				"percepciones_iibb_alicuota": "0",
				"percepciones_iva": "0",
				"percepciones_iva_base": "0",
				"percepciones_iva_alicuota": "0",
				"exentos": "0",
				"impuestos_internos": "0",
				"impuestos_internos_base": "0",
				"impuestos_internos_alicuota": "0"

			}

		},

		{
			"apitoken": "xxxxx",
			"apikey": "xxxxx",
			"usertoken": "xxxxx",
			"cliente": {
				"documento_tipo": "CUIT",
				"condicion_iva": "M",
				"domicilio": "Av Sta Fe 23132",
				"condicion_pago": "211",
				"documento_nro": "3071229384",
				"razon_social": "VOUSYS",
				"provincia": "2",
				"email": "email@dominio.com",
				"envia_por_mail": "N"
			},
			"comprobante": {
				"rubro": "Sevicios web",
				"percepciones_iva": 0,
				"tipo": "FACTURA B",
				"external_reference": "ABC125",
				"numero": 0,
				"percepciones_iibb": 0,
				"bonificacion": 0,
				"operacion": "V",
				"detalle": [{
					"cantidad": 1,
					"producto": {
						"descripcion": "Hosting pagina web ",
						"codigo": 37,
						"lista_precios": "standard",
						"leyenda": "",
						"unidad_bulto": 1,
						"alicuota": 21,
						"precio_unitario_sin_iva": 114.88
					}
				}],
				"fecha": "28/03/2022",
				"rubro_grupo_contable": "Sevicios",
				"total": 139.0,
				"cotizacion": 1,
				"moneda": "PES",
				"punto_venta": 3,
				"percepciones_iibb": "0",
				"percepciones_iibb_base": "0",
				"percepciones_iibb_alicuota": "0",
				"percepciones_iva": "0",
				"percepciones_iva_base": "0",
				"percepciones_iva_alicuota": "0",
				"exentos": "0",
				"impuestos_internos": "0",
				"impuestos_internos_base": "0",
				"impuestos_internos_alicuota": "0"

			}
		}
	]
}
```
{% endcode %}

### **¿Que te retornaremos ?**

#### :red\_circle: Error de validación, de los datos enviados en el lote:

En el caso de un error en la etapa de validación de los datos enviados, el lote no se procesará y obtendrás la respuesta al instante. No se te notificará vía webhook.

Ejemplo de una llamada con 3 requests, donde el segundo el comprobante enviado, tiene el número de comprobante, el lote no se procesará y obtendrás el siguiente error:

{% code title="JSON" %}
```
{
	"error": "S",
	"errores": [
		"El request enviado en el orden 1 (comenzando en 0) tiene el numero de comprobante y todos deben venir en cero. El lote no se procesara."
	],
	"error_cod": [],
	"error_details": []
}
```
{% endcode %}

#### :green\_circle: Cuando el lote se ha aceptado para su procesamiento:

En caso que no se detecten errores tempranos, en la etapa de validación de los datos enviados en el lote, obtendrás la respuesta a cada request enviado, en su mismo orden y luego de enviarte ésta información, recibirás un [webhook](../webhooks-notificaciones.md) por cada request enviado, para informarte que se ha encolado, como se explica a continuación.

Ejemplo de un lote enviado, con 3 requests:

```
{
	"error": "N",
	"errores": [],
	"response": [
		{
			"error": "N",
			"errores": [],
			"cae": " ",
			"cae_vencimiento": null,
			"observaciones": "",
			"envio_x_mail": "N",
			"envio_x_mail_direcciones": "",
			"tfc_generacion_tipo": 3,
			"external_reference": 17032,
			"rta": "El comprobante  se ha guardado correctamente ",
			"vencimiento_cae": "01\/01\/2000",
			"vencimiento_pago": "16\/03\/2022",
			"comprobante_nro": "00010-00000000",
			"comprobante_tipo": "FACTURA A",
			"afip_codigo_barras": "",
			"afip_qr": "",
			"comprobante_pdf_url": ""
		},
		{
			"error": "N",
			"errores": [],
			"cae": " ",
			"cae_vencimiento": null,
			"observaciones": "",
			"envio_x_mail": "N",
			"envio_x_mail_direcciones": "",
			"tfc_generacion_tipo": 3,
			"external_reference": "1453_01",
			"rta": "El comprobante  se ha guardado correctamente ",
			"vencimiento_cae": "01\/01\/2000",
			"vencimiento_pago": "18\/03\/2022",
			"comprobante_nro": "00010-00000000",
			"comprobante_tipo": "FACTURA B",
			"afip_codigo_barras": "",
			"afip_qr": "",
			"comprobante_pdf_url": ""
		},
		{
			"error": "N",
			"errores": [],
			"cae": " ",
			"cae_vencimiento": null,
			"observaciones": "",
			"envio_x_mail": "N",
			"envio_x_mail_direcciones": "",
			"tfc_generacion_tipo": 3,
			"external_reference": "1453_02",
			"rta": "El comprobante  se ha guardado correctamente ",
			"vencimiento_cae": "01\/01\/2000",
			"vencimiento_pago": "18\/03\/2022",
			"comprobante_nro": "00010-00000000",
			"comprobante_tipo": "FACTURA A",
			"afip_codigo_barras": "",
			"afip_qr": "",
			"comprobante_pdf_url": ""
		}
	]
}
```



## Webhooks de respuesta&#x20;

Existen 3 tipos de evento posible, para el recurso de facturación que podes recibir en ésta instancia:  "encolado", "emitido" y "error". Te sugerimos conocer más sobre los webhooks, en la documentación de [Webhooks (notificaciones)](../webhooks-notificaciones.md).

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

&#x20;

