---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para emitir
  comprobantes de venta desde tu sistema actual.
---

# Facturación individual e instantánea

Una vez configurada tu cuenta y creado tu CUIT+PDV, podrás comenzar a emitir facturas electrónicas. Te sugerimos revisar el apartado de [¿Cómo empiezo?](como-empiezo.md)

En TusFacturasAPP, contamos con 2 modalidades para la emisión de comprobantes:

* Facturas individuales instantáneas: donde envías un solo request para ser procesado y obtenes la respuesta al instante (se detalla a continuación).
* Lote de facturas instantáneas: donde envías una cierta cantidad de requests para ser procesados y obtenes la respuesta al instante. Conocé más sobre la [facturación electrónica en lotes, aquí.](api-factura-electronica-afip-api-facturacion-por-lotes.md#facturacioninstantaneaporlotes)

{% hint style="info" %}
**ATENCIÓN!** A partir de abril 2022, éste servicio se modificará para brindarte una solución con muchas más herramientas. Consultanos para más información
{% endhint %}

## ¿Qué puedo facturar?

Podes enviar a facturar cualquier tipo de comprobante A,B,C,E, M y comprobantes de tipo "MiPyme, ya sean facturas, notas de crédito, notas de débito y hasta facturas-recibos.

&#x20;¿No sabes qué [tipo de comprobante debes emitir](que-tipos-de-comprobante-debo-puedo-emitir.md)? Consultalo [desde aquí](que-tipos-de-comprobante-debo-puedo-emitir.md)

Tenés alguna duda del servicio? checkea las [API FAQs](faqs-or-preguntas-frecuentes.md), y si no encontrás lo que buscabas, contactanos por los canales de atención que tenemos disponibles en la plataforma web [www.tusfacturas.app](https://www.tusfacturas.app)



## **Facturación instantánea individual**

Al utilizar éste servicio, los comprobantes que emitas, impactarán de inmediato en nuestra plataforma y obtendrás la respuesta al instante (siempre y cuando los servicios de AFIP se encuentren funcionando).

{% hint style="danger" %}
Es importante que controles los errores, dado que los servicios de AFIP se caen muy seguido y según funcionen sus servicios, la generación de un comprobante puede llegar a demorar hasta 1,30 minutos 😰.
{% endhint %}

A donde debes enviar el request:&#x20;

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/nuevo" method="post" summary="Nuevo comprobante de Venta" %}
{% swagger-description %}
Charset: UTF-8

Tipo de dato esperado: JSON 
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
Estructura de "comprobante" según se informa a continuación
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cliente" type="object" required="false" %}
Estructura de "Cliente", según se informa a continuación
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}
{% endswagger %}



### Ejemplo de JSON para generar un comprobante.

```
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"cliente"   :
                {   "documento_tipo":       "DNI",
                    "documento_nro":        "1292963535",
                    "razon_social":         "Pirulo",
                    "email":                "test@test.com",
                    "domicilio":            "Av Sta Fe 123",
                    "provincia":            "2",
                    "envia_por_mail":       "S",
                    "condicion_pago":       "214",
                    "condicion_pago_otra":  "Cobrado en ventanilla",
                    "condicion_iva":        "CF"
                },

"comprobante":  {

                "fecha":                    "28\/07\/2015",
                "tipo":                     "NOTA DE DEBITO B",
                "moneda":                   "DOL",
               "idioma":                   "1",
                "cotizacion":               "15.20",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6",
                "periodo_facturado_desde":  "27\/07\/2015",
                "periodo_facturado_hasta":  "30\/07\/2015",
                "vencimiento":              "30\/08\/2015",
                "rubro":                    "Servicios web",
                "external_reference":       "ABC123",
                "rubro_grupo_contable":     "servicios",
                "abono": "S",
                "abono_frecuencia": "2",
                "abono_hasta":"10/2019",
                "abono_actualiza_precios": "N",
                "detalle":
                            [
                                {
                                    "cantidad":"1",
                                    "afecta_stock": "N",
                                     "bonificacion_porcentaje": "0",
                                    "producto":
                                            {"descripcion":     "PAPAS",
                                             "unidad_bulto":    "10",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "",
                                             "precio_unitario_sin_iva":"100.45",
                                             "alicuota":      "21",
                                             "impuestos_internos_alicuota": 0,
                                             "unidad_medida": "7",
                                             "actualiza_precio": "S"
                                             },
                                    "leyenda":"blanca, cepillada"
                                },


                                {
                                    "cantidad":"1.5",
                                     "bonificacion_porcentaje": "0",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "HUEVOS",
                                             "unidad_bulto":    "30",
                                             "lista_precios":   "MAPPLETS",
                                             "codigo":          "MPH",
                                             "precio_unitario_sin_iva":"50",
                                             "alicuota":      "10.5",
                                             "impuestos_internos_alicuota": 0,
                                             "unidad_medida": "7",
                                             "actualiza_precio": "N"
                                             },
                                    "leyenda":""
                                },

                                {
                                    "cantidad":"2",
                                     "bonificacion_porcentaje": "0",
                                    "afecta_stock": "S",
                                    "producto":
                                            {"descripcion":     "ZANAHORIA",
                                             "unidad_bulto":    "50",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "ZNH1",
                                             "precio_unitario_sin_iva":"200",
                                             "alicuota":      "21",
                                             "impuestos_internos_alicuota": 0,
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":""
                                }

                            ],
            "rg_especiales":
                 {   "regimen" : "RG 4004-E",
                      "datos"  : 

                           [{
                               "id"      :    17,
                               "valor"  :    "2"
                            },
                            {
                              "id"      :    1801,
                             "valor"  :    "111111111111"
                             },
                            {
                              "id"      :    1802,
                             "valor"  :    "PRUEBA"
                             }]
                },  
                "pagos" : 
                      {
                   	"formas_pago" : [ 
                   			{"descripcion" : "VISA DB", "importe" : 0.6},
                   			{"descripcion" : "MercadoPago", "importe" : 50}
                   			], 
                   	"total": 50.6
                      },                                                               
                "bonificacion":             "120",
                "leyenda_gral":             "Segun Orden de compra III1333",
                "comentario":               "Factura correspondiente al servicio XX",
                "percepciones_iibb":        "0",
                "percepciones_iibb_base":   "0",
                "percepciones_iibb_alicuota": "0",
                "percepciones_iva":         "0",
                "percepciones_iva_base":    "0",
                "percepciones_iva_alicuota": "0",
                "exentos":                  "0",
                "impuestos_internos":       "0",
                "impuestos_internos_base":   "0",
                "impuestos_internos_alicuota": "0",
                "total":                    "543.22" 
                
        }
}

```

### Que te retorna la llamada a la API?

#### &#x20;:white\_check\_mark: Cuando el request resultó exitoso:

Obtendrás la siguiente respuesta, con todos los datos que necesitas para almacenar la info en tu sistema.

La respuesta incluye el texto que se necesita para armar el código QR (en caso que generes el PDF desde tu lado) y/o el viejo código de barras (para comprobantes anteriores).&#x20;

{% hint style="info" %}
Te sugerimos descargar el pdf y almacenarlo en tu plataforma, ya que si tu cuenta o suscripción no se encuentran activas, no podrás obtenerlo.
{% endhint %}

```
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
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
```

#### :octagonal\_sign: Response con error

En caso de detectar error, la variable "error" contendrá una "S" y "errores" una lista con todos los errores encontrados

```
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



### Datos para tener en cuenta:

{% hint style="info" %}
* El CAE es el Código de Autorización Electrónico que otorga AFIP, como confirmación de la creación del comprobante. Es un dato importante para almacenar como respuesta.
* Los CAE tienen fecha de vencimiento y se devuelve en formato dd/mm/aaaa
* Por cuestiones de seguridad, el número de CAE es un texto y se envía con un espacio al final, el cual sugerimos eliminar de tu lado.
* Por cuestiones de seguridad, el texto que se retorna en el campo afip\_codigo\_barras y afip\_qr, se envía con un espacio al final, el cual sugerimos eliminar de tu lado.
* Para evitar inconsistencias en la validación de las sumatorias, te sugerimos redondear los valores decimales con "Round half even".
{% endhint %}

### ¿Cómo determino, si debo emitir un comprobante de tipo "MiPyme"?

Hay ciertos casos donde AFIP exige que en lugar de emitir una factura A,B o C, le emitas a tu cliente, un comprobante de tipo  "FACTURA DE CREDITO ELECTRONICA MiPyME (FCE)" A, B o C. En ese caso, recibirás en la respuesta, el campo requiere\_fec = "SI".&#x20;

Ésto se debe a que el emisor o el receptor están informados como Pyme en AFIP y/o el monto del comprobante a emitir supera el límite que AFIP tiene definido. Ésta info varia día a día, pero disponemos de un método para que puedas invocarlo, previo a éste servicio para conocerlo. Consultá la documentación [desde aquí](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce).&#x20;

Te sugerimos comentar ésta modalidad, con tu cliente y asesorarte con su estudio impositivo al respecto.

## Estructura del bloque: "Comprobante"

Para poder generar un comprobante de tipo factura A,B, C, debes enviar de todos los datos según se informa a continuación:

{% code title="JSON" %}
```
   "comprobante":  {

                "fecha":                    "28\/07\/2015",
                "tipo":                     "FACTURA B",
                "moneda":                   "DOL",
               "idioma":                   "1",
                "cotizacion":               "15.20",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6",
                "periodo_facturado_desde":  "27\/07\/2015",
                "periodo_facturado_hasta":  "30\/07\/2015",
                "vencimiento":              "30\/08\/2015",
                "rubro":                    "Servicios web",
                "rubro_grupo_contable":     "servicios",
                "abono": "S",
                "abono_frecuencia": "2",
                "abono_hasta":"10/2019",
                "abono_actualiza_precios": "N",
                "external_reference":       "ABC123",
                "detalle":
                            [
                                {
                                    "cantidad":"1",
                                    "bonificacion_porcentaje": "0",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "PAPAS",
                                             "unidad_bulto":    "10",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "",
                                             "precio_unitario_sin_iva":"100.45",
                                             "alicuota":      "21",
                                             "unidad_medida": "7",
                                             "impuestos_internos_alicuota": 0,
                                             "actualiza_precio": "S"
                                             },
                                    "leyenda":"blanca, cepillada"
                                },


                                {
                                    "cantidad":"1.5",
                                    "afecta_stock": "N",
                                     "bonificacion_porcentaje": "0",
                                    "producto":
                                            {"descripcion":     "HUEVOS",
                                             "unidad_bulto":    "30",
                                             "lista_precios":   "MAPPLETS",
                                             "codigo":          "MPH",
                                             "precio_unitario_sin_iva":"50",
                                             "alicuota":      "10.5",
                                             "impuestos_internos_alicuota": 0,
                                             "unidad_medida": "7",
                                             "actualiza_precio": "N"
                                             },
                                    "leyenda":""
                                },

                                {
                                    "cantidad":"2",
                                    "afecta_stock": "S",
                                     "bonificacion_porcentaje": "0",
                                    "producto":
                                            {"descripcion":     "ZANAHORIA",
                                             "unidad_bulto":    "50",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "ZNH1",
                                             "precio_unitario_sin_iva":"200",
                                             "alicuota":      "21",
                                             "impuestos_internos_alicuota": 0,
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":""
                                }

                            ],
                "bonificacion":             "120",
                "leyenda_gral":             "Segun Orden de compra III1333",
                "comentario":               "Factura correspondiente al servicio XX",
                "percepciones_iibb":        "0",
                "percepciones_iibb_base":   "0",
                "percepciones_iibb_alicuota": "0",
                "percepciones_iibb_juridiccion": "10",
                "percepciones_iva":         "0",
                "percepciones_iva_base":    "0",
                "percepciones_iva_alicuota": "0",
                "exentos":                  "0",
                "impuestos_internos":       "0",
                "impuestos_internos_base":   "0",
                "impuestos_internos_alicuota": "0", 
                "total":                    "543.22",
                "comprobantes_asociados":    []
        }
```
{% endcode %}

{% hint style="info" %}
Importante: **TusFacturas.app NO válida que la sumatoria de los ítems que estas enviando para facturar se correspondan con los totales. Es responsabilidad del cliente corroborar y validar éstos datos.**

Recordá que **AFIP recibe únicamente totales**, no el detalle de los items que facturás, ya que para los comprobantes de tipo "A" , "B" , "C" y "M" , Factura de crédito electrónica , TusFacturas.app utiliza el método de facturación mediante webservice AFIP "WSFEv1" ( Factura electrónica sin detalle de productos ).
{% endhint %}

#### Información de los campos a enviar:

| Nombre del campo                |         Es requerido?         | Comentarios                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------- | :---------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| fecha                           |               SI              | Campo fecha. Para facturación afip deberá ser la fecha del día. Formato esperado: dd/mm/aaaa. Ejemplo: 13/05/2018                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| tipo                            |               SI              | Campo alfabético según [tabla de referencia de Tipos de comprobantes](tablas-de-referencia.md#tipos-de-comprobantes).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| operacion                       |               SI              | Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| idioma                          |               SI              | Campo numérico. Longitud 1 caracter. Indica el idioma en que se imprimira el PDF del comprobante. Valores Permitidos: 1 = Español, 2= Ingles                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| punto\_venta                    |               SI              | Campo numérico entero. Longitud máxima 5 digitos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| moneda                          |               SI              | Campo alfanumérico de 3 Digitos según [tabla de referencia de Monedas](tablas-de-referencia.md#monedas) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| cotizacion                      |               SI              | Campo numérico con 2 decimales. Puede obtener la cotización del día según AFIP desde nuestro método de consulta de cotización Ejemplo: 15.20                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| numero                          |            OPCIONAL           | El numero del comprobante a generar. Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante contra AFIP. Si el nro de comprobante NO es enviado, traeremos la próxima numeración . Ejemplo: 4567                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| vencimiento                     |            OPCIONAL           | Campo fecha, formato esperado: dd/mm/aaaa. Si no se envía la fecha de vencimiento del pago, se calculará en base a la condición de pago del cliente, contra la fecha del comprobante. En caso que quieras enviar vos, la a de vencimiento, debes indicarlo aca.                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| periodo\_facturado\_desde       |               SI              | Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y asi lo indiquen en la configuración de su CUIT+punto de venta. Obligatorio para quienes facturen Servicios o Productos y Servicios.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| periodo\_facturado\_hasta       |               SI              | Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y así lo indiquen en la configuración de su CUIT+punto de venta.Obligatorio para quienes facturen Servicios o Productos y Servicios.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| rubro                           |               SI              | Campo alfanumérico. Longitud máxima 255 caracteres. Indica el rubro al cual pertenecerá el comprobante. Ésta información no saldrá impresa en el comprobante.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| rubro\_grupo\_contable          |               SI              | Campo alfanumérico. Longitud máxima 255 caracteres. Indica el grupo contable al que pertenece el rubro. Ésta información no saldrá impresa en el comprobante.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| abono                           |            OPCIONAL           | Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si el comprobante a generar es un abono recurrente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| abono\_frecuencia               | REQUERIDO SOLO SI ENVIA ABONO | Campo numerico sin decimales. Indica la frecuencia en meses con la que debe generarse la recurrencia del abono.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| abono\_hasta                    | REQUERIDO SOLO SI ENVIA ABONO | Campo fecha (mm/yyyy). Longitud maxima 7. Indica el mes y año hasta el cual debe generarse el abono recurrente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| abono\_actualiza\_precios       | REQUERIDO SOLO SI ENVIA ABONO | Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si cada vez que se genera el abono, se actualiza los precios de los productos contra el precio actual de la lista de precios.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| detalle                         |               SI              | Lista de conceptos a facturar. [Objeto JSON](api-factura-electronica-afip-facturacion-nuevo-comprobante.md#estructura-de-detalle-de-conceptos) Según estructura que se detalla a continuación                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| fex                             | REQUERIDO PARA COMPROBANTES E | Solo para comprobantes de tipo E. Según estructura detallada en: [Factura electronica de exportacion".](api-factura-electronica-afip-factura-electronica-afip-exportacion.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| bonificacion                    |            OPCIONAL           | Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor aplicado en concepto de bonificación sin IVA Ejemplo: 12.67. Tener en cuenta para el cálculo que la bonificación se aplica sobre el primer subtotal SIN IVA y se lo gravará con el importe de IVA que le corresponda.                                                                                                                                                                                                                                                                                                                                                                                                         |
| leyenda\_gral                   |            OPCIONAL           | Campo alfanumérico. Longitud máxima 255 caracteres. Contenido opcional. Es una leyenda general que saldrá impresa en el bloque central de productos del comprobante Ejemplo: Aplica plan 12 cuotas sin interes. Ten en cuenta que a partir del 01-07-2021, todo comprobante A que se emita a un monotributista deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618"._ Éste valor no debe ser enviado en el campo "leyenda\_gral", ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma. |
| comentario                      |            OPCIONAL           | Campo alfanumerico, opcional. Longitud máxima: 255 caracteres. Éste campo no saldrá impreso en la factura.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| percepciones\_iibb              |            OPCIONAL           | Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de ingresos brutos realizada Ejemplo: 142.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| percepciones\_iibb\_base        |            OPCIONAL           | La base imponible sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| percepciones\_iibb\_alicuota    |            OPCIONAL           | La alícuota sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| percepciones\_iibb\_juridiccion |            OPCIONAL           | La juridicción a la que pertenece la percepción aplicada. El valor a enviar corresponde al ID de la [provincia, según nuestra tabla de referencias.](tablas-de-referencia.md#provincias)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| percepciones\_iva               |            OPCIONAL           | Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de IVA realizada Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| percepciones\_iva\_base         |            OPCIONAL           | La base imponible sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| percepciones\_iva\_alicuota     |            OPCIONAL           | La alícuota sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| impuestos\_internos             |            OPCIONAL           | Indica el valor monetario correspondiente a los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| impuestos\_internos\_base       |            OPCIONAL           | La base imponible sobre la cual se calcularon los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| impuestos\_internos\_alicuota   |            OPCIONAL           | La alícuota sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| exentos                         |            OPCIONAL           | Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de exentos. Solo para comprobantes A y M Ejemplo: 72.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| total                           |               SI              | Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la sumatoria de conceptos incluyendo IVA e impuestos. Ejemplo: 12452.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| comprobantes\_asociados         |       SEGUN CORRESPONDA       | Lista de comprobantes asociados. Requerido únicamente para NC o ND de tipo A,B,C,M. [Objeto JSON](api-factura-electronica-afip-facturacion-nuevo-comprobante.md#estructura-de-comprobantes-asociados) Según estructura que se detalla a continuación                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| rg\_especiales                  |       SEGUN CORRESPONDA       | Lista de datos adicionales requeridos por AFIP, según la RG a la que aplique el comprobante. [Objeto JSON](api-factura-electronica-afip-facturacion-nuevo-comprobante.md#estructura-de-rg-especiales) Según estructura que se detalla a continuación                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| external\_reference             |            OPCIONAL           | Dato alfanumérico de hasta 256 caracteres, que se para referenciar éste comprobante dentro de tu sistema.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

### Estructura del bloque: "Cliente"

Para poder generar el comprobante, debes enviar un detalle de todos los datos del cliente según se informa a continuación.

```
{   
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
"condicion_iva":        "CF"
}
```

### Datos a tener en cuenta:

{% hint style="info" %}
* Si el cliente ya existe en tu base de clientes de TusFacturasAPP, será actualizado con los nuevos datos, salvo los campos de: tipo de documento, número de documento y condición ante el IVA.
* Si queres enviar un comprobante a un consumidor final, sin especificar su nombre y DNI, podes enviar:

Nro de documento = "0"

Tipo de documento = "OTRO"

En nombre, indicá lo que tu contador/a te recomiende.

Tené en cuenta, que solo podrás facturar sin indicar el documento del comprador, hasta ciertos montos que AFIP actualiza regularmente. TusFacturasAPP, cuenta con un método que te permite obtener el monto actualizado. [Consultá la documentaión de los documento : los topes de venta a CF](https://developers.tusfacturas.app/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final)
{% endhint %}

#### Información de los campos a enviar:

| **`documento_tipo`**  | <p>Valores Permitidos: <strong>CUIT , DNI, PASAPORTE, OTRO</strong><br><strong>Ejemplo: DNI</strong></p>                                                                                                                                                                              |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `documento_nro`       | <p>Campo numérico, sin puntos ni guiones.</p><p>Para casos de clientes del exterior, que posean <strong>pasaporte</strong>, ten en cuenta que AFIP solo permite el envío de números. Longitud máxima: 11 digitos.<br><strong>Ejemplo: 30111222334</strong></p>                        |
| `razon_social`        | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Pirulo S.A</strong></p>                                                                                                                                                                                    |
| `email`               | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: tusfacturas@vousys.com</strong></p>                                                                                                                                                                        |
| `domicilio`           | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Av. Santa Fe 123</strong></p>                                                                                                                                                                              |
| `provincia`           | <p>Campo numérico según <a href="tablas-de-referencia.md#provincias">tabla de referencia(*)</a>.<br><strong>Ejemplo: 2</strong></p>                                                                                                                                                   |
| `envia_por_mail`      | <p>Indica Si/No para el envio del comprobante por e-mail. Valores Permitidos: <strong>S , N</strong><br><strong>Ejemplo: S</strong></p>                                                                                                                                               |
| `condicion_pago`      | <p>Campo numérico según <a href="tablas-de-referencia.md#condiciones-de-venta">tabla de referencia</a>.</p><ul><li>se debe enviar obligatoriamente el campo <strong>condicion_pago_otra</strong> "con la descripción de la misma.</li></ul><p><br><strong>Ejemplo: 211 .</strong></p> |
|                       |                                                                                                                                                                                                                                                                                       |
| condicion\_pago\_otra | Campo alfanumerico. Longitud máxima 100 caracteres. **Ejemplo: Cobrado en ventanilla.**                                                                                                                                                                                               |
| `condicion_iva`       | <p>Campo numérico que indica la condicion de iva, según <a href="tablas-de-referencia.md#condiciones-ante-el-iva">tabla de referencia Condiciones ante el IVA(**)</a>. Valores Permitidos: <strong>CF, RI, M, E</strong><br><strong>Ejemplo: RI</strong></p>                          |
| codigo                | Campo alfanumerico opcional. Longitud máxima 50 caracteres. **Ejemplo: Cobrado en ventanilla.**                                                                                                                                                                                       |

###

### Estructura del bloque: "Detalle de conceptos"

El detalle de conceptos se compone de una lista de cada uno de los productos que vas a facturar.

{% hint style="info" %}
Recuerda que debes enviar una **lista (array)** de conceptos. **El máximo de conceptos permitidos por comprobante es de 130**.
{% endhint %}

La estructura **de cada concepto** a enviar es la siguiente:

{% code title="JSON" %}
```
{
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
		"actualiza_precio":"S"
	},
	"leyenda": ""
}
```
{% endcode %}

Los campos que debes enviar son los siguientes:

| `cantidad`               | <p>Campo numérico con 2 decimales. Separador de decimales: punto.<br><strong>Ejemplo: 1.50</strong></p>                                                                          |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `afecta_stock`           | <p>Campo alfanumérico de 1 posición. Valores posibles: "S" (si), "N" (no)<br><strong>Ejemplo: S</strong></p>                                                                     |
| `producto`               | Según estructura de producto                                                                                                                                                     |
| `leyenda`                | <p>Campo alfanumérico. Longitud máxima 100 caracteres. Contenido opcional. Será una descripción que acompañe al producto.<br><strong>Ejemplo: Blanca, cepillada</strong></p>     |
| bonificacion\_porcentaje | Si se ha aplicado un porcentaje de descuento sobre éste concepto, debe ser enviado. Es un campo númerico con 2 decimales. El separador de decimales esperado es el punto. Ej: 25 |
|                          |                                                                                                                                                                                  |
|                          |                                                                                                                                                                                  |

## Estructura del bloque: "Concepto / Producto"

Cada producto o servicio que factures, deberá ser enviado con la siguiente estructura:

```
{
"descripcion":     "HUEVOS",
"unidad_bulto":    "30",
"lista_precios":   "MAPPLETS",
"codigo":          "MPH",
"precio_unitario_sin_iva":"50",
"alicuota":      "10.5",
"unidad_medida": "7",
"impuestos_internos_alicuota": 0,
"actualiza_precio": "N"
}
```

### Datos a tener en cuenta:

{% hint style="info" %}
* Si el producto ya existía en tu base de productos de nuestra plataforma ( se valida que sea la misma lista de precios, código de producto y/o descripción del mismo), el mismo será actualizado por completo, con los nuevos datos que envíes, solo  si indicas que deseas actualizar el precio con el campo "actualiza\_precio":"S".  En caso de no querer actualizar el producto, si el mismo ya existía, se facturará con el nuevo precio y descripción que envíes, pero mantendrá sus datos anteriores.
* Si el comprobante que envias a facturar es de tipo C, todos sus productos no deben llevar IVA, y debes enviar cada concepto con su precio final
* Si el comprobante que envías, es de tipo A o B, los productos o servicios que envíes a facturar, deben ser enviados siempre SIN IVA, porque el IVA se calcula del lado de nuestra plataforma en base al campo "alicuota" que envías. Conocé más de los tipos de comprobantes, [desde aquí ](que-tipos-de-comprobante-debo-puedo-emitir.md)
* En caso que alguno de tus conceptos cuente con un signo porcentual (%) en el nombre (ej:  Promo 20% OFF)  deberás reemplazarlo por los siguientes caracteres: **#\&#**&#x20;
* En caso que alguno de tus conceptos cuente con una nueva línea, en su nombre, o porque deba imprimirse en 2 líneas, deberás generar el salto de línea donde desees, ingresando los caracteres:  **#@#**&#x20;
{% endhint %}

Los campos que debes enviar son los siguientes:

| `descripcion`                 | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Papa blanca</strong></p>                                                                                                                                                                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `unidad_bulto`                | <p>Campo numérico entero requerido. Indica la cantidad de unidades que componen un bulto. Valor minimo esperado: 1<br><strong>Ejemplo: 12</strong></p>                                                                                                                                                                    |
| `lista_precios`               | <p>Campo alfanumérico. Longitud máxima 255 caracteres. Nombre de la lista de precios a la cual pertenece. No saldrá impreso en la factura pero es requerido.<br><strong>Ejemplo: Verdura Orgánica</strong></p>                                                                                                            |
| `codigo`                      | <p>Campo alfanumérico. Longitud máxima 10 caracteres. campo Opcional<br><strong>Ejemplo: ABX780</strong></p>                                                                                                                                                                                                              |
| `precio_unitario_sin_iva`     | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                                                                                                                                                                  |
| `alicuota`                    | <p>Indica la alicuota de IVA con la que grava ese producto. Valores Permitidos:</p><p><strong>27, 21 , 10.5 , 0 , -1 ( para exento), -2 (no gravados)</strong><br><strong>Ejemplo: 10.5</strong></p>                                                                                                                      |
| `unidad_medida`               | <p>Campo numérico que indica la unidad de medida, según<a href="tablas-de-referencia.md#productos-unidades-de-medida-afip"> tabla de referencia Unidades de Medida(**).</a><br><strong>Ejemplo: 7</strong></p>                                                                                                            |
| `actualiza_precio`            | Indica si se actualiza el precio del producto y sus datos adicionales (como ser la unidad de medida, código, unidades por bulto y otros datos adicionales), tomando como valor de referencia,la información enviada en el comprobante. Campo Alfabético, de 1 caracter. Valores permitidos: S (si) N (no). **Ejemplo: S** |
| `impuestos_internos_alicuota` | La alícuota que se cobra en concepto de impuestos internos para éste producto. Campo numerico, con 2 decimales. ej: 10.5                                                                                                                                                                                                  |
|                               |                                                                                                                                                                                                                                                                                                                           |

## Estructura de "Comprobantes Asociados"

**Solo para las notas de débito y las notas de crédito**, AFIP requiere de manera obligatoria, que se envíe un bloque de información adicional con "comprobantes asociados". Los comprobantes asociados son aquellos comprobantes que éstas incluyendo para anular o afectar, según corresponda y son datos que posee el emisor del comprobante en cuestión.

A partir del 01/04/2021 existen 2 maneras de informar los comprobantes asociados:

a) Detallando comprobantes asociados

b) Indicando un período de comprobantes asociados.

Podes ver un [ejemplo de comprobante con comprobantes asociados desde aquí](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a)

{% hint style="info" %}
En todos las notas de crédito y/o notas de débito de cualquier tipo ( A,B, C, E y de tipo MiPyme), **éste bloque es obligatorio,** ya sea que lo hagas por período o por detalle de comprobantes**.**
{% endhint %}

### Envío de comprobantes asociados: "detallados"

Para éste tipo de información, es obligatorio enviar el detalle de los comprobantes que se anulan, dentro de un array, en el bloque llamado "**comprobantes\_asociados**", acorde a la estructura que se detalla a continuación para cada comprobante asociado.

Ten en cuenta que AFIP realiza validaciones sobre éstos datos, ya que según lo que facture tu cliente, tiene una cantidad de dias X habiltiados para anularlas.&#x20;

```
comprobante: {
   .... 
   ,comprobantes_asociados:[
           {
             "tipo_comprobante"   :    "FACTURA A",
              "punto_venta"  :    "145",
              "numero" : 12313,
              "comprobante_fecha": "07/07/2019",
              "cuit": 111111111     
            } ,
           {
             "tipo_comprobante"   :    "FACTURA A",
              "punto_venta"  :    "146",
              "numero" : 12314,
              "comprobante_fecha": "08/07/2019",
              "cuit": 111111111     
            } ,   
      ] 
  }
```

Información de los campos a enviar:

| `tipo_comprobante`  | Campo alfabético. Valores esperados según [tabla de tipos de comprobante.](tablas-de-referencia.md#tipos-de-comprobantes)                                              |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `punto_venta`       | <p>Campo numérico entero. Longitud máxima 5 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                |
| `numero`            | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p> |
| `cuit`              | <p>Campo numérico, sin puntos ni guiones. Es el CUIT del emisor del comprobante asociado.<br><strong>Ejemplo: 1111111111</strong></p>                                  |
| `comprobante_fecha` | La fecha del comprobante en formato dd/mm/aaaa. El día y el mes deben tener 2 dígitos.                                                                                 |

### Comprobantes asociados: "por período"

A partir del 01/04/2021, AFIP habilitó la posibilidad de emitir notas de débito y/o crédito indicando un período desde/hasta en lugar del detalle de comprobantes asociados, para todo comprobante de tipo tradicional (A,B,C)

Para utilizar ésta herramienta, **no se debe enviar el bloque de "**_**comprobantes asociados"**_ **y en su lugar debe enviarse un bloque llamado **_**"comprobantes\_asociados\_periodo",**_ el cual debe tener la siguiente estructura:

```
 comprobante: {
   .... 
   ,comprobantes_asociados_periodo: {
        "fecha_desde"   :    "20/11/2020",
        "fecha_hasta"  :    "25/11/2020"  
    }
 } 
```

Se deberá respetar el formato para las fechas que debe ser dd/mm/aaaa (el día y el mes deben tener 2 dígitos).

## Estructura de "RG Especiales" (OPCIONAL)

Si tu empresa o la de tu cliente, operan bajo alguna RG particular, se deberá enviar un array con los datos adicionales, según se especifican en la [tabla de Datos adicionales para RG Especiales](tablas-de-referencia.md#datos-opcionales-para-rg-especiales).

Ten en cuenta que solo podrás aplicar a un [regimen](tablas-de-referencia.md#datos-opcionales-para-rg-especiales) , por cada comprobante que emitas.

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

### Datos a tener en cuenta:

{% hint style="info" %}
* TusFacturasAPP no realiza validaciones sobre éstos campos. Todas las validaciones son realizadas por la propia AFIP en caso que corresponda.
* Si alguno de los items enviados posee un valor vacio, éste item no será procesado.
{% endhint %}

### Información de los campos a enviar en el array de "datos":

| `id`    | Campo númerico. Valores esperados según[Tabla de Datos Opcionales para RG Especiales](tablas-de-referencia.md#datos-opcionales-para-rg-especiales) |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `valor` | Campo alfanumérico.                                                                                                                                |

## Estructura de "pagos" (OPCIONAL) <a href="#estructuradepagos" id="estructuradepagos"></a>

Si quisieras reflejar junto al envío del comprobante, el pago parcial o total del mismo, debes enviar un bloque, dentro del comprobante, llamado "**pagos**" con la estructura como se detalla a continuación.

Los pagos que informes, se usan solo para la gestión interna de nuestra plataforma y tu cliente no lo verá reflejado en el PDF del comprobante que emitiste, ya que el único objetivo que tiene éste bloque es nutrir la cuenta corriente de tu cliente, con el pago realizado.

### Datos a tener en cuenta:

{% hint style="info" %}
* **NO** podrás enviar los siguientes medios de pago: cheques y detalle de retenciones.
* Se realizará una validación del total que se indique, contra la sumatoria de los medios de pago detallados, previo al guardado del comprobante.
* El total de los pagos **NO** debe superar el importe total del comprobante, pero si puede ser inferior, para indicar que el comprobante recibió un pago parcial.
{% endhint %}

### Información de los campos que componen el **bloque "pagos"**

| nombre del campo | Requerido | Detalle                                                                                                  |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| formas\_pago     | SI        | array con multiples items, según estructura que se detalla a continuación                                |
| total            | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p> |

### Información de los campos que componen el **array de  "formas\_pago"**

| nombre del campo | Requerido | Detalle                                                                                                                                                                                 |
| ---------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| descripcion      | SI        | El nombre del medio de pago elegido para cancelar el comprobante. 255 caracteres max. En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente. |
| importe          | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                                |

### Ejemplo del JSON a enviar.

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

##
