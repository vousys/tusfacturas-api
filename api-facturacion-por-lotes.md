---
description: >-
  Mediante éste método podrás enviar lotes de hasta 100 comprobantes en cada
  llamada que realices.
---

# Facturación por Lotes

{% hint style="warning" %}
Éste método estará disponible a partir del 20/11/2018
{% endhint %}

{% hint style="info" %}
Poder utilizar la API debes [estar registrado](https://www.tusfacturas.com.ar/registrarme-factura-electronica.html).

Mientras estés en etapa de testing, configurá tu CUIT con un punto de venta irreal \(Ej: 679\), y usa ese CUIT de prueba para facturar, la respuesta que recibirás es la misma que si facturas contra AFIP, solo que los campos CAE y Vencimiento del CAE te retornaran vacios. Una vez que hayas probado todos los métodos, crea el nuevo CUIT+punto de venta y lo enlazas con AFIP.

Ten en cuenta que al registrarte, te asignamos un plan gratuito que te permite emitir 5 comprobantes por mes y una vez vencido tu período de prueba, debes contratar algún plan API de los que tenemos disponibles aquí .

En caso que requieras 20 días con un plan free para el desarrollo, contáctanos a tusfacturas@vousys.com
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/api" path="/v2/facturacion/lotes" %}
{% api-method-summary %}
Facturación por Lotes
{% endapi-method-summary %}

{% api-method-description %}
Ten en cuenta que no podras enviar comprobantes de tipo E con ésta modalidad.   
  
Charset: UTF-8  
  
Formato esperado: JSON
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="requests" type="array" required=true %}
Según estructura de de cada item \(detallado abajo\).  
Máximo de request que se recibirán por cada llamada: 500
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
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
        "comprobante_pdf_url": "https:\/\/www.tusfacturas.com.ar\/app\/comprobantes\/0000-11111111111-22222222222-1-00003-00000074.pdf"
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
        "comprobante_pdf_url": "https:\/\/www.tusfacturas.com.ar\/app\/comprobantes\/0000-11111111111-22222222222-1-00003-00000075.pdf"
    }]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Estructura de  "requests"

Requests es un array, que contiene cada uno de los comprobantes a emitir.

{% hint style="info" %}
La **cantidad máxima de requests** \(por cada llamada que realices\) debe ser de 100.

Todos los requests de llamada, deben ser del **mismo tipo de comprobant**e.

Los request deben venir **ordenados por número ascendente y por fecha**.
{% endhint %}

La estructura de cada "request" debe ser acorde a los siguientes tipos de comprobante a generar \([comprobantes de tipo A](facturacion-nuevo-comprobante/factura-a-nota-de-debito-a-nota-de-credito-a.md), [comprobantes de tipo B](facturacion-nuevo-comprobante/factura-nota-de-debito-b-nota-de-credito-bb.md), [comprobantes de tipo C](facturacion-nuevo-comprobante/factura-c-nota-de-debito-c-nota-de-credito-c.md)[ ](facturacion-nuevo-comprobante/factura-electronica-afip-exportacion.md)\) . **No podrás enviar comprobantes de tipo E en ésta modalidad.**

#### Validaciones que realizamos antes de enviarlos a procesar:

* Que no se envien más de 100 requests por llamada.
* Las credenciales de acceso enviadas en cada request deben corresponder con las suyas.
* Dentro de cada request, el campo "numero" del comprobante, debe contener el numero del comprobante en cuestion, ya que con él deberás luego relacionarlo en tu sistema y manejar las respuestas.

## Ejemplo de JSON a enviar

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{   
"apitoken": "kkakak208a17cdfc4e4741437baddaa6",
"apikey": "0000",
"usertoken": "a7ahdt5s7725d7fa4f4e63646bc169b",
"requests": [  
            {
                "apitoken": "kkakak208a17cdfc4e4741437baddaa6",
                "cliente": {
                    "documento_tipo": "CUIT",
                    "condicion_iva": "M",
                    "domicilio": "Av Sta Fe 23132",
                    "condicion_pago": "0",
                    "documento_nro": "3071229384",
                    "razon_social": "VOUSYS",
                    "provincia": "2",
                    "email": "tusfacturas@vousys.com",
                    "envia_por_mail": "N"
                },
                "apikey": "0000",
                "comprobante": {
                    "rubro": "Sevicios web",
                    "percepciones_iva": 0,
                    "tipo": "FACTURA B",
                    "numero": 0,
                    "facturacion_lote_id_referencia": "ASD123AW",
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
                    "impuestos_internos": 0
                },
                "usertoken": "a7ahdt5s7725d7fa4f4e63646bc169b"
            },

                        {
                "apitoken": "kkakak208a17cdfc4e4741437baddaa6",
                "cliente": {
                    "documento_tipo": "CUIT",
                    "condicion_iva": "M",
                    "domicilio": "Av Sta Fe 23132",
                    "condicion_pago": "0",
                    "documento_nro": "3071229384",
                    "razon_social": "VOUSYS",
                    "provincia": "2",
                    "email": "tusfacturas@vousys.com",
                    "envia_por_mail": "N"
                },
                "apikey": "0000",
                "comprobante": {
                    "rubro": "Sevicios web",
                    "percepciones_iva": 0,
                    "tipo": "FACTURA B",
                    "numero": 0,
                    "facturacion_lote_id_referencia": "ASD123AW2",
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
                    "impuestos_internos": 0
                },
                "usertoken": "a7ahdt5s7725d7fa4f4e63646bc169b"
            },

            {
                "apitoken": "kkakak208a17cdfc4e4741437baddaa6",
                "cliente": {
                    "documento_tipo": "CUIT",
                    "condicion_iva": "M",
                    "domicilio": "Av Sta Fe 23132",
                    "condicion_pago": "0",
                    "documento_nro": "3071229384",
                    "razon_social": "VOUSYS",
                    "provincia": "2",
                    "email": "tusfacturas@vousys.com",
                    "envia_por_mail": "N"
                },
                "apikey": "0000",
                "comprobante": {
                    "rubro": "Sevicios web",
                    "percepciones_iva": 0,
                    "tipo": "FACTURA B",
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
                    "fecha": "28/03/2018",
                    "rubro_grupo_contable": "Sevicios",
                    "total": 139.0,
                    "cotizacion": 1,
                    "moneda": "PES",
                    "punto_venta": 3,
                    "impuestos_internos": 0
                },
                "usertoken": "a7ahdt5s7725d7fa4f4e63646bc169b"
            }
        ]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Ejemplo de como invocarlo desde PHP

{% code-tabs %}
{% code-tabs-item title="PHP" %}
```text
// ENVIO REQUEST
$url ="https://www.tusfacturas.com.ar/api/v2/facturacion/lotes" ;

$ch = curl_init( $url );
curl_setopt( $ch, CURLOPT_POSTFIELDS,  json_encode($facturacion_json) );
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );

$json_rta_curl =  json_decode(  curl_exec($ch) ) ;  
curl_close($ch);
​
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## **¿Que te retornaremos en caso de error ?**

#### Error de validación de datos / formato:

Ej: una llamada con 3 requests, donde segundo el comprobante enviado tiene un tipo de comprobante diferente.

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
    "error": "S",
    "errores": ["El comprobante enviado en la fila 1 (comenzando en 0) tiene un tipo de comprobante diferente."]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Error de Procesamiento.

{% hint style="warning" %}
En el caso que se envíe a AFIP el lote a procesar y un comprobante venga rechazado, todos los comprobantes subsiguientes del lote, vendrán rechazados.
{% endhint %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
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
        "comprobante_pdf_url": "https:\/\/www.tusfacturas.com.ar\/app\/comprobantes\/0000-11111111111-22222222222-1-00003-00000074.pdf"
    }, {
        "error": "S",
        "errores": [" AFIP Factura electronica, rechazo el comprobante - ERROR: AFIP rechazo la generacion del comprobante Cod: 0", " AFIP Factura electronica, rechazo el comprobante - ERROR: El campo FchServDesde no puede ser posterior al campo FchServHasta. Cod: 10032"],
        "cae": "",
        "comprobante_nro": "00003-00000082",
        "cae_vencimiento": "",
        "observaciones": "",
        "envio_x_mail": "",
        "envio_x_mail_direcciones": ""
    }, {
        "error": "S",
        "errores": [" AFIP Factura electronica, rechazo el comprobante - ERROR: AFIP rechazo la generacion del comprobante Cod: 0"],
        "cae": "",
        "comprobante_nro": "00003-00000083",
        "cae_vencimiento": "",
        "observaciones": "",
        "envio_x_mail": "",
        "envio_x_mail_direcciones": ""
    }]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## FAQs

#### Si falla una emisión del comprobante de un lote, ¿se realiza un rollback de las emitidas hasta el momento en ese lote? ¿Se emite hasta dicha factura? ¿Saltea el comprobante y continúa con el siguiente?

Si un comprobante tiene error, ese comprobante y los siguientes vendrán rechazados. No existe rollback porque se va procesando contra AFIP y generando en nuestra plataforma en el orden en que se reciben.

#### ¿Cuanto es el tiempo promedio que demora enviar 100 comprobantes?

Tenes un promedio de  3  minutos dependiendo de si ademas de generar el comprobante, el mismo debe ser enviado por email de manera automática

#### ¿Hay una reducción de tiempo considerable al emitir los comprobantes de esta forma?

Si, muchisima.

#### ¿Puedo enviar la información sin algún criterio de ordenamiento?

No, los comprobantes deben ser enviados bajo el criterio de:

1. Mismo tipo de comprobante
2. Número de comprobante \(ascendente\)
3. Fecha

