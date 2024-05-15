---
description: >-
  Facturación Electrónica AFIP Simplificada. Emití facturas electrónicas AFIP de
  forma rápida, segura y sencilla con nuestra API. ¡Integrá la facturación
  electrónica en tu sistema de gestión hoy mismo!
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# API Facturación AFIP

<figure><img src="../.gitbook/assets/157.webp" alt=""><figcaption></figcaption></figure>

Nuestra API de facturación AFIP te permite integrar la facturación electrónica directamente en tu plataforma, eliminando la necesidad de lidiar con los complejos webservices de AFIP. TusFacturasAPP es la solución SaaS ideal para tu negocio.

### ¿Cómo empiezo?

Una vez configurada tu cuenta y creado tu CUIT+PDV en TusFacturasAPP, podrás comenzar a emitir facturas electrónicas AFIP Argentina válidas. Te sugerimos revisar el apartado de [¿Cómo empiezo?](../como-empiezo.md)

### ¿Cómo puedo facturar con TusFacturasAPP?&#x20;

En TusFacturasAPP contamos con 4 modalidades para la emisión de comprobantes online; Sin embargo **te recomendamos** utilizar siempre que sea posible, los **métodos de facturación asincrónicos**, ya que los instantáneos dependen de cómo funcionen los servicios de AFIP en el momento de la emisión.

#### **Facturas AFIP individuales  e instantáneas**

Utilizando éste método vos envías un solo request para ser procesado, y obtenes la respuesta al instante (dependes del estado de los servicios de AFIP)

[Conocé más sobre la facturación electrónica individual e instantánea, desde aquí](./#facturacion-instantanea-individual)



#### **Facturas AFIP individuales en cola       **<mark style="color:purple;background-color:yellow;">**RECOMENDADO**</mark> &#x20;

En éste método envías un solo request para ser procesado y  obtenes la respuesta mediante un [webhook](../webhooks-notificaciones.md) (no dependes del estado de los servicios de facturación de AFIP)

Conocé más sobre la [facturación electrónica individual en cola, desde aquí ](api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)



#### **Lote de facturas AFIP instantáneas**

En éste método envías una cierta cantidad de requests para ser procesados y obtenes la respuesta al instante  (dependes del estado de los servicios de AFIP).

Conocé más sobre la [facturación electrónica en lotes, aquí.](api-factura-electronica-afip-api-facturacion-por-lotes.md#facturacioninstantaneaporlotes)



#### **Lote de facturas asincrónico en cola      **<mark style="color:purple;background-color:yellow;">**RECOMENDADO**</mark> &#x20;

En éste método envías una cierta cantidad de requests para ser procesados y obtenés la respuesta mediante un [webhook](../webhooks-notificaciones.md)  (no dependes del estado de los servicios de facturación de AFIP)

Conocé más sobre la [facturación electrónica por lotes en cola](facturacion-asincronica-por-lotes-encolada.md), aquí.



## ¿Qué puedo facturar con la API?

Nuestro servicio API de facturación electrónica AFIP, te permite enviar a facturar  comprobantes de tipo [A](api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md),[B](api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md),[C](api-factura-electronica-afip-factura-nota-de-debito-b-nota-de-credito-bb.md),[E](api-factura-electronica-afip-factura-electronica-afip-exportacion.md), M, comprobantes de tipo "[Factura de crédito MiPyme](api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce.md)", ya sean facturas, notas de crédito, notas de débito y hasta facturas-recibos.&#x20;

&#x20;¿No sabes qué [tipo de comprobante debes emitir](../que-tipos-de-comprobante-debo-puedo-emitir.md)? Consultalo [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md)

Tenés alguna duda del servicio? checkea las [API FAQs](../faqs-or-preguntas-frecuentes.md), y si no encontrás lo que buscabas, contactanos por los canales de atención que tenemos disponibles, en la plataforma web [www.tusfacturas.app](https://www.tusfacturas.app)



#### &#x20;A donde debes enviar el request:&#x20;

## Estructura generica para el envio de un comprobante.

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/XXXXX`

Charset: UTF-8

Tipo de dato esperado: JSON&#x20;

#### Request Body

| Name        | Type   | Description                                                 |
| ----------- | ------ | ----------------------------------------------------------- |
| usertoken   | string | Tus credenciales de acceso                                  |
| apitoken    | string | Tus credenciales de acceso                                  |
| apikey      | string | Tus credenciales de acceso                                  |
| comprobante | object | Estructura de "comprobante" según se informa a continuación |
| cliente     | object | Estructura de "Cliente", según se informa a continuación    |

{% tabs %}
{% tab title="200 " %}
{% code title="JSON" %}
```javascript
{
    "error":     "N",
     "errores": [ ""],    
     "rta":      "El comprobante NOTA DE DEBITO B 0002-00000006 (MI CUIT) se ha guardado correctamente",    
     "cae":      "65301278726386 ",
     "requiere_fec":   "NO ",    
     "vencimiento_cae":"07\/08\/2015",    
     "vencimiento_pago":"27\/08\/2015",    
     "comprobante_pdf_url": "https://www.dominio.com/url",
     "afip_qr" : "https://www.afip.gob.ar/fe/qr/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjAyMC0xMS0xNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjAwMDAzIiwidGlwb0NtcCI6MTEsIm5yb0NtcCI6IjAwMDAwMjQ5IiwiaW1wb3J0ZSI6IjAwMDAwMDAwMDAwMDEwMCIsIm1vbmVkYSI6IlBFUyIsImN0eiI6IjAwMDAwMDAwMDAwMDEwMDAwMDAiLCJ0aXBvRG9jUmVjIjo5OSwibnJvRG9jUmVjIjoiMCIsInRpcG9Db2RBdXQiOiJFIiwiY29kQXV0IjoiNzA0NjY4OTk1OTcwOTEifQ== "
     "afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
     "envio_x_mail": "S",
     "external_reference":"ABC123",
     "comprobante_nro": "0000123",
     "comprobante_tipo": "NOTA DE DEBITO B",
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
  
  
```
{% endcode %}
{% endtab %}
{% endtabs %}

####

#### Ejemplo de JSON generico <mark style="color:purple;">completo con todas las posibles opciones</mark>, para generar un comprobante.

Tené en cuenta que según el tipo de comprobante que emítas, pueden variar los bloques que debes enviar.&#x20;

```json
{
   "usertoken":"xxxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxxx",
   "cliente":{
      "documento_tipo":"DNI",
      "documento_nro":"1292963535",
      "razon_social":"Pirulo",
      "email":"test@test.com",
      "domicilio":"Av Sta Fe 123",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"214",
      "condicion_pago_otra":"Cobrado en ventanilla",
      "condicion_iva":"CF",
      "reclama_deuda": "S",
      "reclama_deuda_dias": 5,
      "reclama_deuda_repite_dias": 10,       
      "rg5329":"N"
   },
   "comprobante":{
      "fecha":"28\/07\/2015",
      "tipo":"NOTA DE DEBITO B",
      "moneda":"DOL",
      "idioma":"1",
      "cotizacion":"15.20",
      "operacion":"V",
      "punto_venta":"2",
      "numero":"6",
      "periodo_facturado_desde":"27\/07\/2015",
      "periodo_facturado_hasta":"30\/07\/2015",
      "vencimiento":"30\/08\/2015",
      "rubro":"Servicios web",
      "external_reference":"ABC123",
      "tags":[
         "etiqueta1",
         "etiqueta2"
      ],
      "rubro_grupo_contable":"servicios",
      "abono":"S",
      "abono_frecuencia":"2",
      "abono_hasta":"10/2019",
      "abono_actualiza_precios":"N",
      "detalle":[
         {
            "cantidad":"1",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"PAPAS",
               "unidad_bulto":"10",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":"100.45",
               "alicuota":"21",
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"S",
               "rg5329":"N"
            },
            "leyenda":"blanca, cepillada"
         },
         {
            "cantidad":"1.5",
            "bonificacion_porcentaje":"0",
            "afecta_stock":"N",
            "producto":{
               "descripcion":"HUEVOS",
               "unidad_bulto":"30",
               "lista_precios":"MAPPLETS",
               "codigo":"MPH",
               "precio_unitario_sin_iva":"50",
               "alicuota":"10.5",
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"N",
               "rg5329":"N"
            },
            "leyenda":""
         },
         {
            "cantidad":"2",
            "bonificacion_porcentaje":"0",
            "afecta_stock":"S",
            "producto":{
               "descripcion":"ZANAHORIA",
               "unidad_bulto":"50",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"ZNH1",
               "precio_unitario_sin_iva":"200",
               "alicuota":"21",
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"S",
               "rg5329":"N"
            },
            "leyenda":""
         }
      ],
      "rg_especiales":{
         "regimen":"Factura de Cr\u00e9dito Electr\u00f3nica MiPyMEs (FCE)",
         "datos":[
            {
               "id":2101,
               "valor":"0170215820000005295250"
            },
            {
               "id":23,
               "valor":"HANDYWAY CARGO S.A"
            },
            {
               "id":27,
               "valor":"SCA"
            }
         ]
      },
      "comprobantes_asociados":[
         {
            "tipo_comprobante":"FACTURA C",
            "punto_venta":"3",
            "numero":"00000349",
            "comprobante_fecha":"03/03/2022",
            "cuit":27285051466
         }
      ],
      "comprobantes_asociados_periodo":{
         "fecha_desde":"20/11/2020",
         "fecha_hasta":"20/12/2020"
      },
      "pagos":{
         "formas_pago":[
            {
               "descripcion":"VISA DB",
               "importe":0.6
            },
            {
               "descripcion":"MercadoPago",
               "importe":50
            }
         ],
         "total":50.6
      },
      "tributos":[
         {
            "tipo":6,
            "regimen":1,
            "base_imponible":1000,
            "alicuota":10,
            "total":100
         }
      ],
      "exentos":"0",
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "bonificacion":"120",
      "leyenda_gral":"Segun Orden de compra III1333",
      "comentario":"Factura correspondiente al servicio XX",
      "total":"573.22"
   }
}
```

_Información de ejemplo - solo para visualizar su estructura -_&#x20;

### Ejemplos de comprobantes según su tipo / letra

| Tipo de comprobante                                                                                                                                   | Ejemplo                                                                                                                |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Factura A, Nota de débito A, Nota de crédito A                                                                                                        | Ver [ejemplo de comprobantes tipo "A"](api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a.md)   |
| Factura B, Nota de débito B, Nota de crédito B                                                                                                        | Ver [ejemplo de comprobantes tipo "B"](api-factura-electronica-afip-factura-nota-de-debito-b-nota-de-credito-bb.md)    |
| Factura C, Nota de débito C, Nota de crédito C                                                                                                        | Ver [ejemplo de comprobantes tipo "C"](api-factura-electronica-afip-factura-c-nota-de-debito-c-nota-de-credito-c.md)   |
| Factura E, Nota de débito E, Nota de crédito E                                                                                                        | Ver [ejemplo de comprobantes tipo "E"](api-factura-electronica-afip-factura-electronica-afip-exportacion.md)           |
| Factura de Crédito Electrónica MiPyme (FCE),  Nota de débito de Crédito Electrónica MiPyme (FCE), Nota de crédito de Crédito Electrónica MiPyme (FCE) | Ver [ejemplo de comprobantes tipo "MiPyme"](api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce.md) |

#### ¿Cómo determinar, si debo emitir un comprobante de tipo "MiPyme" en lugar de una factura A común?

Hay ciertos casos donde AFIP exige que en lugar de emitir una factura A,B o C, le emitas a tu cliente, un comprobante de tipo  "FACTURA DE CREDITO ELECTRONICA MiPyME (FCE)" A, B o C. En ese caso, recibirás en la respuesta, el campo requiere\_fec = "SI".&#x20;

Ésto se debe a que el emisor o el receptor están informados como Pyme en AFIP y/o el monto del comprobante a emitir supera el límite que AFIP tiene definido. Ésta info varia día a día, pero disponemos de un método para que puedas invocarlo, previo a éste servicio para conocerlo. Consultá la documentación [desde aquí](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce) y te sugerimos comentar ésta modalidad, con tu cliente y asesorarte con su estudio impositivo al respecto.





### Que te retorna la llamada a la API?

#### &#x20;:white\_check\_mark: Cuando el request resultó exitoso:

Sea cual sea la modalidad que utilices para facturar, por cada comprobante que emitas, obtendrás la siguiente respuesta, con todos los datos que necesitas para almacenar en tu sistema.&#x20;

{% hint style="warning" %}
Es importante que descargues toda la información junto con el contenido del pdf y lo almacenes en tu plataforma. La URL del PDF es temporal por lo que no podrás recuperarlo desde ese link en otro momento, y ademas si tu cuenta o suscripción no se encuentran vigentes, no podrás volver a obtenerlo. &#x20;
{% endhint %}

```json
{
    "error":     "N",
     "errores": [ ""],    
     "rta":      "El comprobante NOTA DE DEBITO B 0002-00000006 (MI CUIT) se ha guardado correctamente",    
     "cae":      "65301278726386 ",
     "requiere_fec":   "NO ",    
     "vencimiento_cae":"07\/08\/2015",    
     "vencimiento_pago":"27\/08\/2015",    
     "comprobante_pdf_url": "https://www.dominio.com/url",
     "afip_qr" : "https://www.afip.gob.ar/fe/qr/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjAyMC0xMS0xNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjAwMDAzIiwidGlwb0NtcCI6MTEsIm5yb0NtcCI6IjAwMDAwMjQ5IiwiaW1wb3J0ZSI6IjAwMDAwMDAwMDAwMDEwMCIsIm1vbmVkYSI6IlBFUyIsImN0eiI6IjAwMDAwMDAwMDAwMDEwMDAwMDAiLCJ0aXBvRG9jUmVjIjo5OSwibnJvRG9jUmVjIjoiMCIsInRpcG9Db2RBdXQiOiJFIiwiY29kQXV0IjoiNzA0NjY4OTk1OTcwOTEifQ== "
     "afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
     "envio_x_mail": "S",
     "external_reference":  "ABC123",
     "comprobante_nro": "0000123",
     "comprobante_tipo": "NOTA DE DEBITO B",
     "micrositios": {
			"cliente": "url-del-micrositio",
			"descarga":"url-del-micrositio"
		     },
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
```

#### :octagonal\_sign: Response con error

En caso de detectar error, la variable "error" contendrá una "S" y "errores" una lista con todos los errores encontrados

```json
{
  "error": "S",
  "errores": [
   "El tipo de documento enviado no es valido",
    "Para la condicion de IVA seleccionada no se permite realizar comprobantes de tipo B."
  ],
  "external_reference": "ABC123",
  "error_cod": [],
  "error_details": [
    {
      "code": "TFC-8004",
      "text": "Para la condicion de IVA seleccionada no se permite realizar comprobantes de tipo B."
    }
  ]
}
```



#### Datos para tener en cuenta:

{% hint style="info" %}
**CAE (Código de Autorización electrónica de AFIP)**

* El CAE es el Código de Autorización Electrónico que otorga AFIP, como confirmación de la creación del comprobante. Es un dato importante para almacenar como respuesta.
* Los CAE tienen fecha de vencimiento y se devuelve en formato dd/mm/aaaa
* Por cuestiones de seguridad, el número de CAE es un texto y se envía con un espacio al final, el cual sugerimos eliminar de tu lado.

**AFIP CÓDIGO DE BARRAS / QR**

* Por cuestiones de seguridad, el texto que se retorna en el campo afip\_codigo\_barras y afip\_qr, se envía con un espacio al final, el cual sugerimos eliminar de tu lado.
* Atención! El campo afip\_codigo\_barras dejará de ser enviado a partir del 01/01/2024
* La respuesta exitosa, te incluye el texto que se necesita para armar el código QR (en caso que generes el PDF desde tu lado) y/o el viejo código de barras (para comprobantes anteriores).

**NOTAS DE DÉBITO Y CRÉDITO**

* Las notas de débito y crédito requieren que envies obligatoriamente los comprobantes asociados (o su período asociado). [Conocé más desde aquí](./#estructura-de-comprobantes-asociados)

**REDONDEO DE NÚMEROS / SUMATORIAS / TOTALES**

* Para evitar inconsistencias en la validación de las sumatorias, te sugerimos redondear a 2 decimales los valores y aplicar el redondeo con "Round half even". Te dejamos un link para que puedas probar online éste redondeo: [https://roundingcalculator.guru/rounding-half-to-even-calculator/](https://roundingcalculator.guru/rounding-half-to-even-calculator/)
* **TusFacturas.app NO válida la totalidad de los datos enviados como asi tampoco las sumatorias de los ítems que estas enviando para facturar. Es tu responsabilidad corroborar y validar éstos datos antes de enviarlos.**
* **AFIP recibe únicamente totales**, no el detalle de los items que facturas, ya que para los comprobantes de tipo "A" , "B" , "C" y "M" , Factura de crédito electrónica, TusFacturas.app utiliza el método de facturación mediante webservice AFIP "WSFEv1" ( Factura electrónica sin detalle de productos ).

**MICROSITIOS**

* Las URL de los micrositios solo te serán devueltas con datos, si los mismos se encuentran habilitados en tu cuenta. Para configurarlo, ingresá a nuestra plataforma web, menú > mi espacio de trabajo > mis micrositios. Conocé más de los micrositios [desde aquí](https://www.tusfacturas.app/).

**EDICIÓN / ELIMINACIÓN DE COMPROBANTES**&#x20;

* **Aquellos comprobantes que hayan impactado en AFIP, no podrán ser eliminados, sólo pueden ser anulados contablemente, generando una nota de crédito.**
* Ningún comprobante puede ser modificado una vez emitido.
{% endhint %}

## ¿Cómo es la estructura de un request?

### Estructura del bloque: "Comprobante"

#### Información de los campos a enviar:

<table><thead><tr><th width="286.1885936052475">Nombre del campo</th><th width="127.8396361895644" align="center">Es requerido?</th><th>Comentarios</th></tr></thead><tbody><tr><td>fecha</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha. Para facturación afip deberá ser la fecha del día. Formato esperado: dd/mm/aaaa. Ejemplo: 13/05/2018</td></tr><tr><td>tipo</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfabético según <a href="../parametros/tablas-de-referencia.md#tipos-de-comprobantes">tabla de referencia de Tipos de comprobantes</a>.</td></tr><tr><td>operacion</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V</td></tr><tr><td>idioma</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico. Longitud 1 caracter. Indica el idioma en que se imprimira el PDF del comprobante. Valores Permitidos: 1 = Español, 2= Ingles</td></tr><tr><td>punto_venta</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico entero. Longitud máxima 5 digitos.</td></tr><tr><td>moneda</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico de 3 Digitos según <a href="../parametros/tablas-de-referencia.md#monedas">tabla de referencia de Monedas</a> .</td></tr><tr><td>cotizacion</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico con 2 decimales. Puede obtener la cotización del día según AFIP desde nuestro método de consulta de cotización Ejemplo: 15.20</td></tr><tr><td>numero</td><td align="center">OPCIONAL</td><td>El numero del comprobante a generar. Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante contra AFIP. Si el nro de comprobante NO es enviado, traeremos la próxima numeración . Ejemplo: 4567</td></tr><tr><td>vencimiento</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha, formato esperado: dd/mm/aaaa. </td></tr><tr><td>periodo_facturado_desde</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y asi lo indiquen en la configuración de su CUIT+punto de venta. Obligatorio para quienes facturen Servicios o Productos y Servicios.</td></tr><tr><td>periodo_facturado_hasta</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y así lo indiquen en la configuración de su CUIT+punto de venta.Obligatorio para quienes facturen Servicios o Productos y Servicios.</td></tr><tr><td>rubro</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres. Indica el rubro al cual pertenecerá el comprobante. Ésta información no saldrá impresa en el comprobante.</td></tr><tr><td>rubro_grupo_contable</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres. Indica el grupo contable al que pertenece el rubro. Ésta información no saldrá impresa en el comprobante.</td></tr><tr><td>abono</td><td align="center">OPCIONAL</td><td>Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si el comprobante a generar es un abono recurrente.</td></tr><tr><td>abono_frecuencia</td><td align="center"><mark style="color:purple;">REQUERIDO SOLO SI ENVIA ABONO</mark></td><td>Campo numerico sin decimales. Indica la frecuencia en meses con la que debe generarse la recurrencia del abono.</td></tr><tr><td>abono_hasta</td><td align="center"><mark style="color:purple;">REQUERIDO SOLO SI ENVIA ABONO</mark></td><td>Campo fecha (mm/yyyy). Longitud maxima 7. Indica el mes y año hasta el cual debe generarse el abono recurrente.</td></tr><tr><td>abono_actualiza_precios</td><td align="center"><mark style="color:purple;">REQUERIDO SOLO SI ENVIA ABONO</mark></td><td>Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si cada vez que se genera el abono, se actualiza los precios de los productos contra el precio actual de la lista de precios.</td></tr><tr><td>detalle</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Lista de conceptos a facturar. <a href="./#estructura-de-detalle-de-conceptos">Objeto JSON</a> Según estructura que se detalla a continuación</td></tr><tr><td>fex</td><td align="center"><mark style="color:purple;">REQUERIDO PARA COMPROBANTES E</mark></td><td>Solo para comprobantes de tipo E. Según estructura detallada en: <a href="api-factura-electronica-afip-factura-electronica-afip-exportacion.md">Factura electronica de exportacion".</a></td></tr><tr><td>bonificacion</td><td align="center">OPCIONAL</td><td>Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor aplicado en concepto de bonificación sin IVA Ejemplo: 12.67. Tener en cuenta para el cálculo que la bonificación se aplica sobre el primer subtotal SIN IVA y se lo gravará con el importe de IVA que le corresponda.</td></tr><tr><td>leyenda_gral</td><td align="center">OPCIONAL</td><td><p>Campo alfanumérico. Longitud máxima 500 caracteres. Contenido opcional. Es una leyenda general que saldrá impresa en el bloque central de productos del comprobante. Si queres que parte del texto salga en una linea nueva, agrega: #@# , si queres enviar el "%", en su lugar envía: #&#x26;#.</p><p></p><p> Ejemplo: Aplica plan 12 cuotas, con un 10#&#x26;# de interes. </p><p></p><p>Ten en cuenta que a partir del 01-07-2021, todo comprobante A que se emita a un monotributista deberá llevar la siguiente leyenda: "<em>El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618".</em> <strong>Éste valor no debe ser enviado en el campo "leyenda_gral",</strong> ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma.</p></td></tr><tr><td>comentario</td><td align="center">OPCIONAL</td><td>Campo alfanumerico, opcional. Longitud máxima: 255 caracteres. Éste campo no saldrá impreso en la factura.</td></tr><tr><td>tributos</td><td align="center"><mark style="color:orange;">SOLO SI APLICA</mark></td><td>Lista de percepciones y otros impuestos, según se detalla su estructura a continuación.</td></tr><tr><td>impuestos_internos</td><td align="center">OPCIONAL</td><td>Indica el valor monetario correspondiente a los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67</td></tr><tr><td>impuestos_internos_base</td><td align="center">OPCIONAL</td><td>La base imponible sobre la cual se calcularon los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67</td></tr><tr><td>impuestos_internos_alicuota</td><td align="center">OPCIONAL</td><td>La alícuota sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67</td></tr><tr><td>total</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la sumatoria de conceptos incluyendo IVA e impuestos. Ejemplo: 12452.67</td></tr><tr><td>comprobantes_asociados</td><td align="center"><mark style="color:orange;">SOLO PARA NC O ND</mark></td><td>Lista de comprobantes asociados. Requerido únicamente para NC o ND de tipo A,B,C,M. <a href="./#estructura-de-comprobantes-asociados">Objeto JSON</a> Según estructura que se detalla a continuación</td></tr><tr><td>rg_especiales</td><td align="center"><mark style="color:orange;">REQUERIDO SI APLICA ALGUNA RG</mark></td><td>Lista de datos adicionales requeridos por AFIP, según la RG a la que aplique el comprobante. <a href="./#estructura-de-rg-especiales">Objeto JSON</a> Según estructura que se detalla a continuación</td></tr><tr><td>external_reference</td><td align="center"><mark style="color:orange;">SOLO PARA VENTAS ASYNC</mark></td><td>Dato alfanumérico de hasta 255 caracteres (solo se permiten letras, números, guión bajo y guión medio), que se utiliza para referenciar a éste comprobante, dentro de tu sistema. Es opcional, salvo que utilices los métodos de envió a la cola de procesamiento. No se realiza validación de éste campo, para verificar que el mismo no exista.</td></tr><tr><td>tags</td><td align="center">OPCIONAL</td><td>Objeto JSON, según estructura que se detalla a continuación.</td></tr></tbody></table>

### Estructura del bloque: "Cliente"

Para poder generar el comprobante, debes enviar un detalle de todos los datos del cliente según se informa a continuación.

```json
comprobante: {
   .... 
   cliente: {   
      "documento_tipo":       "DNI",
      "documento_nro":        "1292963535",
      "razon_social":         "Pirulo",
      "email":                "test@test.com",
      "domicilio":            "Av Sta Fe 123",
      "provincia":            "2",
      "codigo":               "CLO2",
      "envia_por_mail":       "S",
      "condicion_pago":       "214",
      "condicion_pago_otra":  "Cobrado en ventanilla",
      "condicion_iva":        "CF",
      "reclama_deuda":        "S",
      "reclama_deuda_dias":   5,
      "reclama_deuda_repite_dias": 10,  
      "rg5329":                "N"
   }
}
```



#### Información de los campos a enviar:

<table data-header-hidden><thead><tr><th align="center">NOMBRE DEL CAMPO</th><th width="144.66666666666669" align="center">REQUERIDO?</th><th>INFO</th></tr></thead><tbody><tr><td align="center"><strong><code>documento_tipo</code></strong></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Valores Permitidos: <strong>CUIT , DNI, PASAPORTE, OTRO</strong><br><strong>Ejemplo: DNI</strong></td></tr><tr><td align="center"><code>documento_nro</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico, sin puntos ni guiones.<br><strong>Ejemplo: 30111222334</strong></td></tr><tr><td align="center"><code>razon_social</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Pirulo S.A</strong></td></tr><tr><td align="center"><code>email</code></td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 255 caracteres. Máximo 15 direcciones separadas por coma.<br><strong>Ejemplo: tusfacturas@vousys.com</strong></td></tr><tr><td align="center"><code>domicilio</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres. <br><strong>Ejemplo: Av. Santa Fe 123</strong></td></tr><tr><td align="center"><code>provincia</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico según <a href="../parametros/tablas-de-referencia.md#provincias">tabla de referencia(*)</a>.<br><strong>Ejemplo: 2</strong></td></tr><tr><td align="center"><code>envia_por_mail</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Indica Si/No para el envio del comprobante por e-mail. Valores Permitidos: <strong>S , N</strong><br><strong>Ejemplo: S</strong></td></tr><tr><td align="center"><code>condicion_pago</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Campo numérico según <a href="../parametros/tablas-de-referencia.md#condiciones-de-venta">tabla de referencia</a>.</p><ul><li>se debe enviar obligatoriamente el campo <strong>condicion_pago_otra</strong> "con la descripción de la misma.</li></ul><p><br><strong>Ejemplo: 211 .</strong></p></td></tr><tr><td align="center">condicion_pago_otra</td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 100 caracteres. <strong>Ejemplo: Cobrado en ventanilla.</strong></td></tr><tr><td align="center"><code>condicion_iva</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico que indica la condición de iva, según <a href="../parametros/tablas-de-referencia.md#condiciones-ante-el-iva">tabla de referencia Condiciones ante el IVA(**)</a>. Valores Permitidos: <strong>CF, RI, M, E</strong><br><strong>Ejemplo: RI</strong></td></tr><tr><td align="center">codigo</td><td align="center">OPCIONAL</td><td>Campo alfanumérico opcional. Longitud máxima 50 caracteres. <strong>Ejemplo: Cobrado en ventanilla.</strong></td></tr><tr><td align="center">rg5329</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Este campo te permite indicar si tu cliente es pasible de <a href="../faqs-or-rg5329.md">percepción IVA RG5329</a>.</p><p>Valores posibles: "S" o "N".</p></td></tr><tr><td align="center">reclama_deuda</td><td align="center">OPCIONAL</td><td>Indica SI/No para el envio del <a href="https://www.tusfacturas.app/caracteristicas-de-tus-facturas-electronica-clientes.html">recordatorio de pago</a> al cliente. Opciones validas: "S" o "N"</td></tr><tr><td align="center">reclama_deuda_dias</td><td align="center">OPCIONAL</td><td>En caso de haber habilitado el recordatorio de pago atrasado, se debe indicar cuantos dias pasados la fecha de vencimiento del comprobante se desea comenzar a recordar el pago adeudado. Se espera recibir un valor numerico indicando el número de días)</td></tr><tr><td align="center">reclama_deuda_repite_dias</td><td align="center">OPCIONAL</td><td>En caso de haber habilitado del recordatorio de pago atrasado, se debe indicar la frecuencia de cada cuantos dias se desea volver a recordar. Se espera recibir un valor numérico, indicando el número de días.</td></tr></tbody></table>



{% hint style="info" %}
**Datos a tener en cuenta:**

* Si el cliente ya existe en tu base de clientes de TusFacturasAPP, será actualizado con los nuevos datos, salvo los campos de: tipo de documento, número de documento y condición ante el IVA.
* Si queres facturar un comprobante **a consumidor final, sin especificar su nombre y DNI**, debes enviar en el campo tipo y número de documento, lo siguiente:

Nro de documento = "0"

Tipo de documento = "OTRO"

En nombre, indicá lo que tu contador/a te recomiende.

Tené en cuenta, que solo podrás facturar sin indicar el documento del comprador, hasta ciertos montos que AFIP actualiza regularmente. TusFacturasAPP, cuenta con un método que te permite obtener el monto actualizado. [Consultá la documentación: los topes de venta a CF](https://developers.tusfacturas.app/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final)

* Para casos de clientes del exterior, que posean **pasaporte**, tené en cuenta que AFIP sólo permite el envío de números.&#x20;
{% endhint %}

###

### Estructura del bloque: "Detalle de conceptos"

El detalle de conceptos se compone de una lista de cada uno de los productos o servicios que vas a facturar.

{% hint style="info" %}
&#x20;**El máximo de conceptos permitidos por comprobante es de 130**.
{% endhint %}

La estructura **de la lista de conceptos** a enviar es la siguiente:

{% code title="JSON" %}
```json
comprobante: {
   .... 
   detalle: [{
	"cantidad": "1.5",
	"afecta_stock": "N",
	"bonificacion_porcentaje": "0",
	"producto": {
		"descripcion": "HUEVOS",
		"unidad_bulto": "30",
		"lista_precios": "MAPPLETS",
		"codigo": "MPH",
		"precio_unitario_sin_iva": "50",
		"impuestos_internos_alicuota": 0,
		"alicuota": "10.5",
		"unidad_medida": "7",
		"actualiza_precio":"S",
		"rg5329": "S"
	},
	"leyenda": ""
       },
       {
	"cantidad": "3",
	"afecta_stock": "S",
	"bonificacion_porcentaje": "50",
	"producto": {
		"descripcion": "PALITOS SALADOS",
		"unidad_bulto": "30",
		"lista_precios": "SNACKS",
		"codigo": "PLi",
		"precio_unitario_sin_iva": "50",
		"impuestos_internos_alicuota": 0,
		"alicuota": "10.5",
		"unidad_medida": "7",
		"actualiza_precio":"S",
		"rg5329": "N"
	},
	"leyenda": "En paquetes de 190gr"
       }
      ]
   } 
```
{% endcode %}

Los campos que debes enviar en cada concepto de la lista del bloque "detalle" son los siguientes:

<table data-header-hidden><thead><tr><th width="242.66666666666666">NOMBRE DEL CAMPO</th><th width="157" align="center">REQUERIDO?</th><th></th></tr></thead><tbody><tr><td><code>cantidad</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico con 2 decimales. Separador de decimales: punto.<br><strong>Ejemplo: 1.50</strong></td></tr><tr><td><code>afecta_stock</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico de 1 posición. Valores posibles: "S" (si), "N" (no)<br><strong>Ejemplo: S</strong></td></tr><tr><td><code>producto</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Según estructura de producto que se detalla en el bloque siguiente.</td></tr><tr><td><code>leyenda</code></td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 100 caracteres. Contenido opcional. Será una descripción que acompañe al producto.<br><strong>Ejemplo: Blanca, cepillada</strong></td></tr><tr><td><mark style="background-color:purple;">bonificacion_porcentaje</mark></td><td align="center">OPCIONAL</td><td>Si se ha aplicado un porcentaje de descuento sobre éste concepto, debe ser enviado. Es un campo númerico con 2 decimales. El separador de decimales esperado es el punto. Ej: 25</td></tr></tbody></table>

### Estructura del bloque: "detalle->producto"

Cada producto o servicio que factures, deberá ser enviado con la siguiente estructura:

<pre class="language-json"><code class="lang-json">{
    "descripcion":     "HUEVOS",
<strong>    "unidad_bulto":    "30",
</strong>    "lista_precios":   "MAPPLETS",
    "codigo":          "MPH",
    "precio_unitario_sin_iva":"50",
    "alicuota":      "10.5",
    "unidad_medida": "7",
    "impuestos_internos_alicuota": 0,
    "actualiza_precio": "N",
    "rg5329": "N"
}
</code></pre>



{% hint style="info" %}
**Datos a tener en cuenta:**

* Si el producto ya existía en tu base de productos de nuestra plataforma ( se valida que sea la misma lista de precios, código de producto y/o descripción del mismo), el mismo será actualizado por completo, con los nuevos datos que envíes, solo  si indicas que deseas actualizar el precio con el campo "actualiza\_precio":"S".  En caso de no querer actualizar el producto, si el mismo ya existía, se facturará con el nuevo precio y descripción que envíes, pero mantendrá sus datos anteriores.
* Si el comprobante que envías a facturar es de tipo C, todos los productos/conceptos que factures no deben llevar IVA y deberás enviar cada concepto con su precio final
* Si el comprobante que envías, es de tipo A o B, los productos o servicios que envíes a facturar, deben ser enviados siempre SIN IVA, porque el IVA se calcula del lado de nuestra plataforma en base al campo "alicuota" que envías. Conocé más de los tipos de comprobantes, [desde aquí ](../que-tipos-de-comprobante-debo-puedo-emitir.md)
* En caso que alguno de tus conceptos cuente con un signo porcentual (%) en el nombre (ej:  Promo 20% OFF)  deberás reemplazarlo por los siguientes caracteres: **#\&#**&#x20;
* En caso que alguno de tus conceptos cuente con una nueva línea, en su nombre, o porque deba imprimirse en 2 líneas, deberás generar el salto de línea donde desees, ingresando los caracteres:  **#@#**&#x20;
* **Cómo calcular el IVA:**
  *   Si necesitas calcular cuánto vale tu producto sin IVA, te dejamos un cálculo rápido:&#x20;

      Precio del producto con 21% de IVA = 121

      Para saber el precio sin el 21% de IVA debes hacer:  121 / 1.21  = 100
  * Si quisieras saber cuanto es el precio de tu producto + 21% de IVA, debes hacer el siguiente cálculo:

&#x20;            Precio del producto sin 21% de IVA = 100

&#x20;            Para saber el precio con el 21% de IVA debes hacer:  100 x 1.21 = 121


{% endhint %}



Los campos que debes enviar son los siguientes:

<table data-header-hidden><thead><tr><th width="335.66666666666663">NOMBRE DEL CAMPO</th><th width="145" align="center">REQUERIDO?</th><th>INFO</th></tr></thead><tbody><tr><td><code>descripcion</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres y mínima de 4 caracteres.<br><strong>Ejemplo: Papa blanca</strong></td></tr><tr><td><code>unidad_bulto</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico entero requerido. Indica la cantidad de unidades que componen un bulto. Valor minimo esperado: 1<br><strong>Ejemplo: 12</strong></td></tr><tr><td><code>lista_precios</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud mínima de 4 caracteres y máxima 255 caracteres. Nombre de la lista de precios a la cual pertenece. No saldrá impreso en la factura pero es requerido.<br><strong>Ejemplo: Verdura Orgánica</strong></td></tr><tr><td><code>codigo</code></td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 10 caracteres. Si bien el campo es opcional, es recomendable enviarlo.<br><strong>Ejemplo: ABX780</strong></td></tr><tr><td><code>precio_unitario_sin_iva</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></td></tr><tr><td><code>alicuota</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Indica la alícuota de IVA con la que grava ese producto. Valores Permitidos:</p><p><strong>27, 21 , 10.5 , 0 , -1 ( para exento), -2 (no gravados)</strong><br><strong>Ejemplo: 10.5</strong></p></td></tr><tr><td><code>unidad_medida</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico que indica la unidad de medida, según<a href="../parametros/tablas-de-referencia.md#productos-unidades-de-medida-afip"> tabla de referencia Unidades de Medida(**).</a><br><strong>Ejemplo: 7</strong></td></tr><tr><td><code>actualiza_precio</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Indica si se actualiza el precio del producto y sus datos adicionales (como ser la unidad de medida, código, unidades por bulto y otros datos adicionales), tomando como valor de referencia,la información enviada en el comprobante. Campo Alfabético, de 1 carácter. Valores permitidos: S (si) N (no). <strong>Ejemplo: S</strong></td></tr><tr><td><code>impuestos_internos_alicuota</code></td><td align="center">OPCIONAL</td><td>La alícuota que se cobra en concepto de impuestos internos para éste producto. Campo numérico, con 2 decimales. ej: 10.5</td></tr><tr><td>rg5329</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Este campo te permite indicar si tu producto percibe la percepción IVA RG5329.</p><p>Valores posibles: "S" o "N".</p><p>Si envias el valor en "S", debes enviar el campo "actualiza_precio" tambien en "S".</p><p>Conocé cuando aplicar la RG5329 <a href="../faqs-or-rg5329.md">desde aquí</a></p></td></tr></tbody></table>



### Estructura de "Comprobantes Asociados"

Encontrá la estructura e información de éste bloque desde la sección "[Notas de crédito/Notas de débito](api-factura-electronica-afip-notas-credito-debito.md)"

**Existen 2 maneras de informar los comprobantes asociados:**

a) Detallando los comprobantes asociados que anulas.

b) Indicando un período de comprobantes asociados.&#x20;



### Estructura del bloque: "tributos"&#x20;

Cuando requieras enviar percepciones de IVA o percepciones de Ingresos Brutos (IIBB) deberás enviar dentro del bloque "comprobante", un array con la siguiente estructura:&#x20;

Ejemplo:&#x20;

<pre class="language-json"><code class="lang-json">		 
<strong> "tributos": [	
</strong>			{
				"tipo" : 7,
				"regimen": 22,
				"base_imponible": 2000,
				"alicuota": 20,
				"total": 400				
			}, 		
			{
				"tipo" : 6,
				"regimen": 3,
				"base_imponible": 1000,
				"alicuota": 3,
				"total": 30
			}, 		
			{
				"tipo" : 6,
				"regimen": 3,
				"base_imponible": 1000,
				"alicuota": 1.5,
				"total": 15	
			},
			{
				"tipo" : 6,
				"regimen": 1,
				"base_imponible": 1000,
				"alicuota": 10,
				"total": 100
			}
		],  
</code></pre>

#### Información de los campos a enviar dentro de cada "tributo":

<table><thead><tr><th width="248">nombre del campo</th><th width="133.66666666666669">REQUERIDO</th><th>Valores esperados</th></tr></thead><tbody><tr><td>tipo</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico, según tabla de referencia <a data-mention href="../parametros/tablas-de-referencia.md#bloque-tributos-greater-than-tipos-de-percepcion-a-aplicar">#bloque-tributos-greater-than-tipos-de-percepcion-a-aplicar</a></td></tr><tr><td>regimen</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico, según tabla de referencia: <a data-mention href="../parametros/tablas-de-referencia.md#bloque-tributos-greater-than-regimen-de-percepcion">#bloque-tributos-greater-than-regimen-de-percepcion</a></td></tr><tr><td>base_imponible</td><td><mark style="color:purple;">REQUERIDO</mark></td><td> Campo numérico con hasta 2 decimales, donde se indica la base imponible sobre la cual se aplica la percepción.</td></tr><tr><td>alicuota</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico con hasta 2 decimales, donde se indica la alícuota de dicha percepción</td></tr><tr><td>total</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico de hasta 2 decimales, con el importe total de la percepción a aplicar.</td></tr></tbody></table>





### Estructura de "RG Especiales"&#x20;

Si la empresa, opera bajo alguna RG particular, se deberá enviar un array con los datos adicionales, según se especifican en la [tabla de Datos adicionales para RG Especiales](../parametros/tablas-de-referencia.md#datos-opcionales-para-rg-especiales).

Ten en cuenta que solo podrás aplicar a un solo [regimen](../parametros/tablas-de-referencia.md#datos-opcionales-para-rg-especiales) , por cada comprobante que emitas.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "rg_especiales":   
  {   "regimen" : "RG 4004-E",
      "datos"  : 
               [{
                   "id"      :    18,
                   "valor"  :    "PRUEBA "
                },
                {
                  "id"      :    19,
                 "valor"  :    "PRUEBA (2) "
                 }]
   } 
 }
```
{% endcode %}

#### Datos a tener en cuenta:

{% hint style="info" %}
* TusFacturasAPP no realiza validaciones sobre éstos campos. Todas las validaciones son realizadas por la propia AFIP en caso que corresponda.
* Si alguno de los items enviados posee un valor vacio, éste item no será procesado.
{% endhint %}

#### Información de los campos a enviar en el array de "datos":

<table data-header-hidden><thead><tr><th width="214"></th><th width="151.66666666666669">REQUERIDO</th><th></th></tr></thead><tbody><tr><td><code>id</code></td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo númerico. Valores esperados según <a href="../parametros/tablas-de-referencia.md#datos-opcionales-para-rg-especiales">Tabla de Datos Opcionales para RG Especiales</a></td></tr><tr><td><code>valor</code></td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico.</td></tr></tbody></table>

### &#x20;<a href="#estructuradepagos" id="estructuradepagos"></a>

### Estructura de "pagos"   <a href="#estructuradepagos" id="estructuradepagos"></a>

Si quisieras reflejar junto al envío del comprobante, el pago parcial o total del mismo, debes enviar un bloque, dentro del comprobante, llamado "**pagos**" con la estructura como se detalla a continuación. **Éste bloque es opcional.**

Los pagos que informes, se usan solo para la gestión interna de nuestra plataforma y tu cliente no lo verá reflejado en el PDF del comprobante que emitiste, ya que el único objetivo que tiene éste bloque es nutrir la cuenta corriente de tu cliente, con el pago realizado.

#### Datos a tener en cuenta:

{% hint style="info" %}
* **NO** podrás enviar los siguientes medios de pago: cheques y detalle de retenciones.
* Se realizará una validación del total que se indique, contra la sumatoria de los medios de pago detallados, previo al guardado del comprobante.
* El total de los pagos **NO** debe superar el importe total del comprobante, pero si puede ser inferior, para indicar que el comprobante recibió un pago parcial.
{% endhint %}

#### Información de los campos que componen el **bloque "pagos"**

<table><thead><tr><th>Nombre del campo</th><th width="141.66666666666669" align="center">REQUERIDO</th><th>Detalle</th></tr></thead><tbody><tr><td>formas_pago</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>array con multiples items, según estructura que se detalla a continuación</td></tr><tr><td>total</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></td></tr></tbody></table>

#### Información de los campos que componen el **array de  "formas\_pago"**

| Nombre del campo |                   Requerido                  | Detalle                                                                                                                                                                                 |
| ---------------- | :------------------------------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| descripcion      | <mark style="color:purple;">REQUERIDO</mark> | El nombre del medio de pago elegido para cancelar el comprobante. 255 caracteres max. En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente. |
| importe          | <mark style="color:purple;">REQUERIDO</mark> | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                                |

#### Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "pagos" : 
   {
	"formas_pago" : [ 
			{"descripcion" : "VISA DB", "importe" : 0.6},
			{"descripcion" : "MercadoPago", "importe" : 50}
			], 
	"total": 50.6
   }, 
 }
```
{% endcode %}



### Estructura de "tags"

{% hint style="info" %}
Éste bloque se incorporará a partir del 01/04/2022
{% endhint %}

Si quisieras enviar tags para agregar a tus comprobantes, a modo de etiqueta informativa, debés enviar un array con el nombre de cada una de éstas.

Cada tag, debe ser un campo alfanumérico de hasta 255 caracteres y puedes enviar hasta 50 tags por comprobante.

#### Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "tags" :  [ "etiqueta1", "etiqueta2"],   
 }
```
{% endcode %}





