---
description: >-
  Mediante éste método podrás enviar, lotes de request con comprobantes de
  venta, configurando la fecha de generación, y a medida que se generan, te
  notificamos vía un webhook.
---

# Facturación por lotes \(Async + programado + webhook\)

{% hint style="info" %}
Atencion! éste método está deshabilitado por el momento.
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/api" path="/v2/facturacion/lotes" %}
{% api-method-summary %}
Facturación por Lotes
{% endapi-method-summary %}

{% api-method-description %}
Ten en cuenta que no podras enviar comprobantes de tipo E con ésta modalidad.Charset: UTF-8  
Formato esperado: JSON
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="fecha\_envio\_inicial" type="string" required=false %}
La fecha a partir de cuando se quiere comenzar a enviar los comprobantes.  
La fecha no puede ser inferior a hoy.  
Si la fecha no es enviada se tomara la del día actual.  
Importante: Ésta fecha NO sobre-escribe la fecha que se indica en cada comprobante. Tener en cuenta que AFIP no permite emitir comprobantes con menos de 10 días y si ya existe una fecha posterior. Ej. Emiti la factura con fecha \(HOY\) y luego envío a generar una factura con fecha \(AYER\). retornará error desde AFIP.Formato esperado: dd/mm/aaaa
{% endapi-method-parameter %}

{% api-method-parameter name="webhook\_url" type="string" required=true %}
La URL donde te notificaremos de cada comprobante que se ha generado. Formato esperado: https://www.tudominio.com
{% endapi-method-parameter %}

{% api-method-parameter name="requests" type="array" required=true %}
Según estructura de de cada item, detallado abajo.  
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
En caso de exito, retorna la cantidad que proceso y la info de los registros que NO proceso.
{% endapi-method-response-example-description %}

```text
{"error":"N",
"errores":[],
"procesados": 5,
"validaciones":
["El usertoken del comprobante enviado en la fila 0 (comenzando en 0) no se corresponde con sus credenciales. No se enviará a generar",
"El usertoken del comprobante enviado en la fila 1 (comenzando en 0) no se corresponde con sus credenciales. No se enviará a generar",
"El usertoken del comprobante enviado en la fila 2 (comenzando en 0) no se corresponde con sus credenciales. No se enviará a generar"]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## ¿Como funciona el modo asincrónico de facturación por lote?

![](../.gitbook/assets/image.png)

{% hint style="success" %}
El modo asincrónico puede ser usado para enviar tanto un comprobante, como un lote de hasta 500 comprobantes; ya que fue pensado para optimizar los procesos de generación de los mismos.
{% endhint %}

## ¿Qué es un WebHook?

Un `webhook` es una notificación que se envía de un servidor a otro mediante una llamada `HTTP POST` al ocurrir un determinado evento.

TusFacturas usa `webhooks` para comunicarte los eventos que ocurren en relación a tu solicitud de generación de ventas. El `webhook` debe retornar a TusFacturas con un `HTTP Status 200` ó `201`.

### **¿Que te retornaremos via webhook?**

Vas a recibir por POST un JSON con la siguiente estructura, para que puedas relacionar mediante el ID que nos enviaste como referencia, al comprobante en cuestión:

{% code title="JSON" %}
```text
{
"error":"N",
"errores":[],
"rta":"El comprobante FACTURA B 0003-00000007 (XXXX) se ha guardado correctamente ",
"cae":"XXXXXXXX ",
"vencimiento_cae":"01\/01\/2000",
"vencimiento_pago":"28\/03\/2018",
"comprobante_nro":"0003-00000007",
"comprobante_tipo":"FACTURA B",
"observaciones": "",
"envio_x_mail":"N",
"comprobante_pdf_url":"https:\/\/www.dominio.com/XXXXXX.pdf",
"facturacion_lote_id_referencia":"ASD123AW",
"apikey":"1234",
"apitoken":"7adshadh716781b4e4741437baddaa6",
"usertoken":"DASADDSnjshdgasjh711231"

}
```
{% endcode %}

{% hint style="info" %}
Ten en cuenta que dentro de la captura del webhook, deberás realizar las validaciones correspondientes desde tu lado \(que apikey, apitoken, usertoken te correspondan, que el id de referencia se corresponda, etc\)
{% endhint %}

### Estructura de  "requests"

Requests es un array, que contiene cada uno de los comprobantes a emitir.

El limite máx de request por llamada que esperamos recibir es 500.

La estructura de cada "request" debe ser acorde a los siguientes tipos de comprobante a generar \([comprobantes de tipo A](../api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md), [comprobantes de tipo B](../api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-nota-de-debito-b-nota-de-credito-bb.md), [comprobantes de tipo C](../api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-c-nota-de-debito-c-nota-de-credito-c.md)[ ](../api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-electronica-afip-exportacion.md)\) con la salvedad de que debe agregarse el campo `facturacion_lote_id_referencia`, dentro de la [estructura JSON de "comprobante" ](../api-factura-electronica-afip-facturacion-nuevo-comprobante/#ejemplo-de-json-que-debes-enviar) y el campo `numero` debe ser enviado en cero, de modo que se genere la numeración correlativa a medida que se procesa. **No podrás enviar comprobantes de tipo E en ésta modalidad.**

#### Validaciones que realizamos en ésta etapa:

* Que se envíe una URL válida para el wehbook.
* Que no se envien más de 500 requests por llamada.
* Las credenciales de acceso enviadas en cada request deben corresponder con las suyas.
* Dentro de cada request, el campo "numero" del comprobante, debe estar en cero.
* Dentro de cada request, el comprobante  debe recibir un valor para facturacion\_lote\_id\_referencia con contenido. TusFacturas NO validará si el mismo se encuentra duplicado.
* No validamos en ésta etapa, que el comprobante tenga todos los datos válidos.

#### ¿Que pasa si un comprobante tiene error?

Intentaremos generar cada comprobante, máximo de 10 veces. En caso de superar esa cantidad, te enviaríamos el webhook con la respuesta de error, de la misma manera que recibís con la generación instantánea de comprobantes.

### Ejemplo de JSON a enviar

{% code title="JSON" %}
```text
{   
"apitoken": "kkakak208a17cdfc4e4741437baddaa6",
"apikey": "1235",
"usertoken": "a7ahdt5s7725d7fa4f4e63646bc169b",
"webhook_url": "https://www.tusfacturas.app",
"fecha_envio_inicial": "29/03/2018",
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
                "apikey": "1235",
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
                "apikey": "1235",
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
                "apikey": "1235",
                "comprobante": {
                    "rubro": "Sevicios web",
                    "percepciones_iva": 0,
                    "tipo": "FACTURA B",
                    "numero": 0,
                    "facturacion_lote_id_referencia": "ASD123AW3",
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
{% endcode %}

### Ejemplo de como invocarlo desde PHP

{% code title="PHP" %}
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
{% endcode %}

## ¿Que necesito hacer para migrar desde comprobantes instantáneos?

Si ya venias haciendo comprobantes instantáneos y queres migrar a la facturación asincrónica para acelerar los tiempos de procesamiento, estos son los puntos que deberías tener en cuenta:

1- Necesitas crearte un script del lado de tu servidor, para que reciba el JSON con los eventos que enviaremos [via webhook](nuevo-comprobante-de-venta-async.md#que-te-retornaremos-via-webhook) \(ya sean por resultado exitoso o con error\).

2- Agregá las validaciones necesarias de tu lado, para corroborar que la info recibida es tuya y corresponde ser procesada \(ej: Vallidacion de apikey, apitoken, usertoken y id de referencia enviado\)

3- Modificá tu llamada actual a nuestra API, para usar "facturacion/lotes" en lugar de "facturacion/nuevo"

4- [Modificá en tu JSON con el reques](nuevo-comprobante-de-venta-async.md#estructura-de-requests)[t](nuevo-comprobante-de-venta-async.md#estructura-de-requests) a enviar, para que el campo "numero" del comprobante, llegue en cero y agregá el campo: "facturacion\_lote\_id\_referencia" con tu ID interno, para poder machearlo.

5- Modificá la llamada a nuestra API para que [tenga la estructura definida previamente](nuevo-comprobante-de-venta-async.md#facturacion-por-lotes)

## FAQs

#### Si falla una emisión del comprobante de un lote, ¿se realiza un rollback de las emitidas hasta el momento en ese lote? ¿Se emite hasta dicha factura? ¿Saltea el comprobante y continúa con el siguiente?

Saltea el comprobante y continúa con el siguiente dado que los comprobantes que envíes NO tienen numeración asignada. Un comprobante que no pudo ser procesado porque hubo error , se intenta re-procesar hasta 15 veces.

#### ¿Que problemas puedo encontrar?

Por ej si enviaste un lote de 5 facturas , con diferente fecha, y se fueron procesando en el orden enviado, con el siguiente estado:

* Factura 1  \(10/01/2018\) - PROCESADA Y FACTURADA
* Factura 2  \(10/01/2018\) - PROCESADA Y FACTURADA
* Factura 3  \(15/01/2018\) - PROCESADA CON ERROR
* Factura 4  \(16/01/2018\) - PROCESADA Y FACTURADA
* Factura 5  \(18/01/2018\) - PENDIENTE

Cuando se reintente procesar la FACTURA 3, la AFIP va a retornar error, ya que se HA emitido una factura con fecha posterior.

#### ¿Hay una reducción de tiempo considerable al emitir los comprobantes de esta forma?

Optimizas porque lo podes dejar programado con anterioridad, podes mandar el lote el dia 5 e indicar que esos comprobantes se emitan el dia 29; ademas tu proceso no se trabaria esperando la respuesta de la factura como si la mandaras instantánea. Sigue con las siguientes y a medida q va procesando te va notificando.

#### En caso de que falle el request del webhook, ¿se realizan reintentos hasta completar la notificación?

La plataforma intentará notificarte a tu webhook hasta 15 veces.

#### ¿Queda registrado en su plataforma para que eventualmente solicitemos un retry?

Queda registrado en la plataforma y podrás solicitar el retry tanto de la generación del comprobante nuevamente, como del envio del webhook.

#### ¿Puedo enviar la información sin algún criterio de ordenamiento?

Debes enviar los comprobantes a facturar en orden, por fecha, ya que se procesa en el orden en que se fue recibiendo.

#### ¿Los comprobantes que envío a facturar, son validados \(en cuanto al formato esperado\) antes de guardarlos?

Actualmente no, pero estamos trabajando para integrar esa funcionalidad sin incrementar el tiempo de procesamiento, cada vez que envíes un lote.

