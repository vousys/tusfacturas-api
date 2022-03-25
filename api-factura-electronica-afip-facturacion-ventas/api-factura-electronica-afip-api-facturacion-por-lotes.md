---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para enviar a
  procesar lotes y obtener la respuesta al instante.
---

# Facturación instantánea por Lotes

{% hint style="info" %}
**ATENCIÓN!** A partir de abril 2022, éste servicio se modificará para brindarte una solución con muchas más herramientas. Consultanos para más información
{% endhint %}

Una vez configurada tu cuenta y creado tu CUIT+PDV, podrás comenzar a emitir facturas electrónicas. Te sugerimos revisar el apartado de [¿Cómo empiezo?](../como-empiezo.md) y luego ["Facturación"](./), para conocer la estructura de cada request que envíes.&#x20;

## ¿Qué puedo facturar por lote?

Podes enviar a facturar comprobantes de tipo A,B,C y M; ya sean facturas, notas de crédito, notas de débito y hasta facturas-recibos. **No podrás enviar comprobantes de tipo E ni de Factura de crédito electrónica (FEC) en ésta modalidad.**

&#x20;¿No sabes qué [tipo de comprobante debes emitir](../que-tipos-de-comprobante-debo-puedo-emitir.md)? Consultalo [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md)

Tenés alguna duda del servicio? checkea las [API FAQs](../faqs-or-preguntas-frecuentes.md), y si no encontrás lo que buscabas, contactanos por los canales de atención que tenemos disponibles en la plataforma web [www.tusfacturas.app](https://www.tusfacturas.app)

## **Facturación instantánea por Lote**

Al utilizar éste servicio, los comprobantes que emitas, impactarán de inmediato en nuestra plataforma y obtendrás la respuesta al instante (siempre y cuando los servicios de AFIP se encuentren funcionando).

{% hint style="danger" %}
Es importante que controles los errores, dado que los servicios de AFIP se caen muy seguido y según funcionen sus servicios, la generación de un comprobante puede llegar a demorar hasta 1,30 minutos 😰. Para evitar éste tipo de problemas, te sugerimos utilizar la [facturación por lotes asincrónica (encolada)](facturacion-asincronica-por-lotes-encolada.md)
{% endhint %}

Es necesario leer primero, la documentación de "[Facturación](./)", para conocer cómo debe componerse cada request que envíes.



{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/facturacion/lotes" method="post" summary="Facturación por Lotes" %}
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
**Datos a tener en cuenta**

* **La cantidad máxima de requests (por lote) debe ser de 20**, pero debes tener en cuenta que por cuestiones de seguridad, nuestra plataforma funciona limitando su tiempo de procesamiento y según funcionen los servicios de AFIP, puedes obtener una respuesta de timeout (524). En caso de recibir un 524, ten en cuenta que los comprobantes que enviaste, seguirán siendo procesados en background, pero no recibirás la respuesta.  Te sugerimos utilizar la modalidad de [Facturación encolada por lotes](facturacion-asincronica-por-lotes-encolada.md) para evitar éste tipo de errores.
* Todos los requests de ésta llamada, deben ser del **mismo tipo de comprobante**. Ej: todos deben ser FACTURA A
* Todos los requests de ésta llamada, deben ser de la **misma fecha**. Ej: todos deben ser 12/03/2021
* Los request deben venir **ordenados por número ascendente**, de la misma manera que si los enviarás a procesar uno por uno.
* **No podrás enviar comprobantes de** [**tipo E**](api-factura-electronica-afip-factura-electronica-afip-exportacion.md) **ni de** [**Factura de crédito electrónica (FEC)**](api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce.md) **en ésta modalidad.**
* Si se detecta al menos un (1) error de validación de datos de nuestro lado, el lote no se mandará a procesar.
{% endhint %}

La estructura de cada "request" debe ser acorde a los siguientes tipos de comprobante a generar ([comprobantes de tipo A](api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md), [comprobantes de tipo B](api-factura-electronica-afip-factura-nota-de-debito-b-nota-de-credito-bb.md), [comprobantes de tipo C](api-factura-electronica-afip-factura-c-nota-de-debito-c-nota-de-credito-c.md)[ ](api-factura-electronica-afip-factura-electronica-afip-exportacion.md)) .

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
				"fecha": "28/03/2018",
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
				"external_reference": "ABC124",
				"numero": 2,
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
				"fecha": "28/03/2018",
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
				"numero": 3,
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
				"fecha": "28/03/2018",
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

#### Ejemplo de como invocarlo desde PHP

{% code title="PHP" %}
```
// ENVIO REQUEST
$url ="https://www.tusfacturas.app/api/v2/facturacion/lotes" ;

$ch = curl_init( $url );
curl_setopt( $ch, CURLOPT_POSTFIELDS,  json_encode($facturacion_json) );
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );

$json_rta_curl =  json_decode(  curl_exec($ch) ) ;  
curl_close($ch);
​
```
{% endcode %}

### **¿Que te retornaremos en caso de error ?**

#### Error de validación de datos / formato:

Ej: una llamada con 3 requests, donde segundo el comprobante enviado tiene un tipo de comprobante diferente.

{% code title="JSON" %}
```
{
    "error": "S",
    "errores": ["El comprobante enviado en la fila 1 (comenzando en 0) tiene un tipo de comprobante diferente."]
}
```
{% endcode %}

#### Error de Procesamiento:

{% hint style="warning" %}
En el caso que se envíe a AFIP el lote a procesar y un comprobante venga rechazado, todos los comprobantes subsiguientes del lote, vendrán rechazados. Ésta funcionalidad está determinada por AFIP.
{% endhint %}

{% code title="JSON" %}
```
 {
    "error": "S",
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
        "comprobante_pdf_url": "https:\/\/www.dominio.com\/074.pdf",
        "external_reference":"AAAA"
    }, {
        "error": "S",
        "errores": [" AFIP Factura electronica, rechazo el comprobante - ERROR: AFIP rechazo la generacion del comprobante Cod: 0", " AFIP Factura electronica, rechazo el comprobante - ERROR: El campo FchServDesde no puede ser posterior al campo FchServHasta. Cod: 10032"],
        "cae": "",
        "comprobante_nro": "00003-00000082",
        "external_reference":"ABC124",
        "cae_vencimiento": "",
        "observaciones": "",
        "envio_x_mail": "",
        "envio_x_mail_direcciones": ""
    }, {
        "error": "S",
        "errores": [" AFIP Factura electronica, rechazo el comprobante - ERROR: AFIP rechazo la generacion del comprobante Cod: 0"],
        "cae": "",
        "comprobante_nro": "00003-00000083",
        "external_reference":"ABC125",
        "cae_vencimiento": "",
        "observaciones": "",
        "envio_x_mail": "",
        "envio_x_mail_direcciones": ""
    }]
}
```
{% endcode %}

## FAQs

#### Si falla una emisión del comprobante de un lote, ¿se realiza un rollback de las emitidas hasta el momento en ese lote? ¿Se emite hasta dicha factura? ¿Saltea el comprobante y continúa con el siguiente?

Si un comprobante tiene error, ese comprobante y los siguientes vendrán rechazados. No existe rollback porque se va procesando contra AFIP y generando en nuestra plataforma en el orden en que se reciben.

#### ¿Hay una reducción de tiempo considerable al emitir los comprobantes de esta forma?

Si.

#### ¿Puedo enviar la información sin algún criterio de ordenamiento?

No, los comprobantes deben ser enviados bajo el criterio de:

1. Mismo tipo de comprobante
2. Número de comprobante (ascendente)
3. Fecha

&#x20;
