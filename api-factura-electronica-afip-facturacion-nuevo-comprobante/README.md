---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para emitir
  comprobantes de venta desde tu sistema actual.
---

# API Factura electrónica AFIP - Comprobantes: Facturación individual de nueva venta

Una vez configurada tu cuenta y creado tu CUIT+PDV, podrás comenzar a emitir facturas electrónicas.

Ten en cuenta que los comprobantes que emitas, impactaran de inmediato en nuestra plataforma y obtendrás la respuesta al instante. 

{% hint style="info" %}
Es importante que controles los errores, dado que los servicios de AFIP se caen muy seguido y ten en cuenta que según funcionen sus servicios, la generación de un comprobante puede llegar a demorar hasta 1,30 minutos 😰.
{% endhint %}

A continuación te mostramos la estructura que debe tener el JSON que envíes:

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/nuevo" method="post" summary="Nuevo comprobante de Venta" %}
{% swagger-description %}
Charset: UTF-8 

\


Tipo de dato esperado: JSON

\


Tipo de envio: POST

\




\


Éste método te permite generar comprobantes de venta, ya sea Facturas electrónicas AFIP, como Notas de débito o de crédito.

\


Nuestra plataforma te permite emitir comprobantes de tipo A, B, C, E, M ya sean de factura electrónica AFIP como de Factura de crédito electrónica MiPyme AFIP.

\



{% endswagger-description %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" type="object" %}
Estructura de "comprobante" según se informa a continuación
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cliente" type="object" %}
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
     "comprobante_nro": "0000123",
     "comprobante_tipo": "NOTA DE DEBITO B",
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
  
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

###

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
			         "pagos" : {
						          "formas_pago" : [ 
										                      {"descripcion" : "VISA DEBITO", "importe" : 0.6}
							                        ], 
							        "total": 0.6
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

#### Éxito

En caso de éxito, obtendrás la siguiente respuesta, con todos los datos que necesitas para almacenar la info en tu sistema. La respuesta incluye el texto que se necesita para armar el  código QR (en caso que generes el PDF desde tu lado) y/o el viejo código de barras (para comprobantes anteriores).

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
     "comprobante_nro": "0000123",
     "comprobante_tipo": "NOTA DE DEBITO B",
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
```

####  Response con error

En caso de detectar error, la variable "error" contendrá una "S" y "errores" una lista con todos los errores encontrados 

```
{
  "error": "S",
  "errores": [
    "Para la condicion de IVA seleccionada no se permite realizar comprobantes de tipo B."
  ],
  "error_cod": [],
  "error_details": [
    {
      "code": "TFC-8004",
      "text": "Para la condicion de IVA seleccionada no se permite realizar comprobantes de tipo B."
    }
  ]
}
```

En caso que el comprobante presente errores ya que debe emitir un comprobante de tipo Factura de crédito electronica MiPyme (FEC), el mismo aparecerá informado con una variable requiere_fec = "SI"

Ten en cuenta:

* El CAE es el Código de Autorización Electrónico que otorga AFIP como confirmación de la creación del comprobante. Es un dato importante para almacenar como respuesta.
* Los CAE tienen fecha de vencimiento y se devuelve en formato dd/mm/aaaa
* El número de CAE es un texto y se envia con un espacio al final.
* El texto que se retorna en el campo afip_codigo_barras y afip_qr, se envía con un espacio al final.

{% hint style="info" %}
Debes tener en cuenta, que según el monto a emitir y/o el receptor de los comprobantes que emitas, AFIP puede exigirte que en lugar de emitir los comprobantes tradicionales de tipo A, B, o C, emitas comprobantes de tipo Factura de crédito electrónica MiPyme. Puedes usar antes de emitir una venta, el [servicio de consulta de Factura de crédito electrónica](../api-factura-electronica-afip-consulta-de-obligado-a-recibir-factura-de-credito-electronica-mipyme.md#consulta-de-obligado-a-recibir-mipyme). Te sugerimos comentarlo con tu cliente y asesorarte con su estudio impositivo al respecto.
{% endhint %}

###

### Estructura de "Comprobante"

Para poder generar el comprobante, debes enviar de todos los datos según se informa a continuación.

{% code title="JSON" %}
```
   
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
                "rubro_grupo_contable":     "servicios",
                "abono": "S",
                "abono_frecuencia": "2",
                "abono_hasta":"10/2019",
                "abono_actualiza_precios": "N",
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
Importante: **TusFacturas.app NO válida que la sumatoria de los ítems que estas enviando para facturar se correspondan con los totales. Es responsabilidad del cliente corroborar y validar éstos datos. **

Recordá que **AFIP recibe únicamente totales**, no el detalle de los items que facturas ya que para los comprobantes de tipo "A" , "B" , "C" y "M" , Factura de crédito electrónica , TusFacturas.app utiliza el método de facturación mediante webservice AFIP "WSFEv1" ( Factura electrónica sin detalle de productos ).
{% endhint %}

#### Información de los campos a enviar:

| Nombre del campo              | Requerido                     | Comentarios                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fecha                         | SI                            | Campo fecha. Para facturación afip deberá ser la fecha del día. Formato esperado: dd/mm/aaaa. Ejemplo: 13/05/2018                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| tipo                          | SI                            | Campo alfabético según [tabla de referencia de Tipos de comprobantes](../tablas-de-referencia.md#tipos-de-comprobantes).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| operacion                     | SI                            | Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| idioma                        | SI                            | Campo numérico. Longitud 1 caracter. Indica el idioma en que se imprimira el PDF del comprobante. Valores Permitidos: 1 = Español, 2= Ingles                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| punto_venta                   | SI                            | Campo numérico entero. Longitud máxima 5 digitos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| moneda                        | SI                            | Campo alfanumérico de 3 Digitos según [tabla de referencia de Monedas](../tablas-de-referencia.md#monedas) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| cotizacion                    | SI                            | Campo numérico con 2 decimales. Puede obtener la cotización del día según AFIP desde nuestro método de consulta de cotización Ejemplo: 15.20                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| numero                        | OPCIONAL                      | El numero del comprobante a generar. Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante contra AFIP. Si el nro de comprobante NO es enviado, traeremos la próxima numeración . Ejemplo: 4567                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| vencimiento                   | OPCIONAL                      | Campo fecha, formato esperado: dd/mm/aaaa. Si no se envía la fecha de vencimiento del pago, se calculará en base a la condición de pago del cliente, contra la fecha del comprobante.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| periodo_facturado_desde       | SI                            | Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y asi lo indiquen en la configuración de su CUIT+punto de venta. Obligatorio para quienes facturen Servicios o Productos y Servicios.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| periodo_facturado_hasta       | SI                            | Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y así lo indiquen en la configuración de su CUIT+punto de venta.Obligatorio para quienes facturen Servicios o Productos y Servicios.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| rubro                         | SI                            |  Campo alfanumérico. Longitud máxima 255 caracteres. Indica el rubro al cual pertenecerá el comprobante. Ésta información no saldrá impresa en el comprobante.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| rubro_grupo_contable          | SI                            |  Campo alfanumérico. Longitud máxima 255 caracteres. Indica el grupo contable al que pertenece el rubro. Ésta información no saldrá impresa en el comprobante.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| abono                         | OPCIONAL                      | Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si el comprobante a generar es un abono recurrente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| abono_frecuencia              | REQUERIDO SOLO SI ENVIA ABONO | Campo numerico sin decimales. Indica la frecuencia en meses con la que debe generarse la recurrencia del abono.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| abono_hasta                   | REQUERIDO SOLO SI ENVIA ABONO | Campo fecha (mm/yyyy). Longitud maxima 7. Indica el mes y año hasta el cual debe generarse el abono recurrente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| abono_actualiza_precios       | REQUERIDO SOLO SI ENVIA ABONO | Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si cada vez que se genera el abono, se actualiza los precios de los productos contra el precio actual de la lista de precios.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| detalle                       | SI                            |  Lista de conceptos a facturar. [Objeto JSON](./#estructura-de-detalle-de-conceptos) Según estructura que se detalla a continuación                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| fex                           | REQUERIDO PARA COMPROBANTES E | Solo para comprobantes de tipo E. Según estructura detallada en: [Factura electronica de exportacion".](api-factura-electronica-afip-factura-electronica-afip-exportacion.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| bonificacion                  | OPCIONAL                      |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor aplicado en concepto de bonificación sin IVA Ejemplo: 12.67. Tener en cuenta para el cálculo que la bonificación se aplica sobre el primer subtotal SIN IVA y se lo gravará con el importe de IVA que le corresponda.                                                                                                                                                                                                                                                                                                                                                                                                         |
| leyenda_gral                  | OPCIONAL                      |  Campo alfanumérico. Longitud máxima 255 caracteres. Contenido opcional. Es una leyenda general que saldrá impresa en el bloque central de productos del comprobante Ejemplo: Aplica plan 12 cuotas sin interes. Ten en cuenta que a partir del 01-07-2021, todo comprobante A que se emita a un monotributista deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618".  _Éste valor no debe ser enviado en el campo "leyenda_gral", ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma. |
| comentario                    | OPCIONAL                      | Campo alfanumerico, opcional. Longitud máxima: 255 caracteres. Éste campo no saldrá impreso en la factura.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| percepciones_iibb             | OPCIONAL                      |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de ingresos brutos realizada Ejemplo: 142.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| percepciones_iibb_base        | OPCIONAL                      | La base imponible  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| percepciones_iibb_alicuota    | OPCIONAL                      | La alícuota  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| percepciones_iibb_juridiccion | OPCIONAL                      | La juridicción a la que pertenece la percepción aplicada. El valor a enviar corresponde al ID de la [provincia, según nuestra tabla de referencias.](../tablas-de-referencia.md#provincias)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| percepciones_iva              | OPCIONAL                      | Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de IVA realizada Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| percepciones_iva_base         | OPCIONAL                      | La base imponible sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| percepciones_iva_alicuota     | OPCIONAL                      | La alícuota  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| impuestos_internos            | OPCIONAL                      | Indica el valor monetario correspondiente a los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| impuestos_internos_base       | OPCIONAL                      | La base imponible  sobre la cual se calcularon los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| impuestos_internos_alicuota   | OPCIONAL                      | La alícuota  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| exentos                       | OPCIONAL                      |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de exentos. Solo para comprobantes A y M Ejemplo: 72.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| total                         | SI                            |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la sumatoria de conceptos incluyendo IVA e impuestos. Ejemplo: 12452.67                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| comprobantes_asociados        | SEGUN CORRESPONDA             | Lista de comprobantes asociados. Requerido únicamente para NC o ND de tipo A,B,C,M. [Objeto JSON](./#estructura-de-comprobantes-asociados) Según estructura que se detalla a continuación                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| rg_especiales                 | SEGUN CORRESPONDA             | Lista de datos adicionales requeridos por AFIP, según la RG a la que aplique el comprobante.  [Objeto JSON](./#estructura-de-rg-especiales) Según estructura que se detalla a continuación                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

{% hint style="info" %}
Si querés que el comprobante tenga una fecha de vencimiento de pago particular, enviala en el campo  "**vencimiento"**.
{% endhint %}

### Estructura de  "Cliente"

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

{% hint style="info" %}
Cuestiones a tener en cuenta:

* Si el cliente ya existia en tu base de clientes, será actualizado con los nuevos datos, salvo los campos de Tipo y Nro de documento y condicion ante el IVA.
* Si queres enviar un comprobante a un consumidor final, sin especificar su nombre y DNI, podes enviar:

                    Nro de documento = "0" 

                    Tipo de documento = "OTRO" 

                     En nombre, lo que tu contador/a te recomiende.  

Ten en cuenta que ésto solo está permitido para comprobantes hasta ciertos          montos. En Marzo 2021 el tope es de $20,932.- , pero éste valor puede sufrir modificaciones. Consultanos el valor actualizado a  hola@tusfacturas.app 
{% endhint %}



#### Información de los campos a enviar:

| **`documento_tipo`** | <p>Valores Permitidos: <strong>CUIT , DNI, PASAPORTE, OTRO</strong><br><strong>Ejemplo: DNI</strong></p>                                                                                                                                                                                   |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `documento_nro`      | <p>Campo numérico, sin puntos ni guiones.  </p><p>Para casos de clientes del exterior, que posean <strong>pasaporte</strong>, ten en cuenta que AFIP solo permite el envío de números.<br><strong>Ejemplo: 30111222334</strong></p>                                                        |
| `razon_social`       | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Pirulo S.A</strong></p>                                                                                                                                                                                         |
| `email`              | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: tusfacturas@vousys.com</strong></p>                                                                                                                                                                             |
| `domicilio`          | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Av. Santa Fe 123</strong></p>                                                                                                                                                                                   |
| `provincia`          | <p>Campo numérico según <a href="../tablas-de-referencia.md#provincias">tabla de referencia(*)</a>.<br><strong>Ejemplo: 2</strong></p>                                                                                                                                                     |
| `envia_por_mail`     | <p>Indica Si/No para el envio del comprobante por e-mail. Valores Permitidos: <strong>S , N</strong><br><strong>Ejemplo: S</strong></p>                                                                                                                                                    |
| `condicion_pago`     | <p>Campo numérico según <a href="../tablas-de-referencia.md#condiciones-de-venta">tabla de referencia</a>.  </p><ul><li>se debe enviar obligatoriamente el campo <strong>condicion_pago_otra</strong> "con la descripción de la misma.</li></ul><p><br><strong>Ejemplo: 211 .</strong></p> |
|                      |                                                                                                                                                                                                                                                                                            |
| condicion_pago_otra  | Campo alfanumerico. Longitud máxima 100 caracteres. **Ejemplo: Cobrado en ventanilla.**                                                                                                                                                                                                    |
| `condicion_iva`      | <p>Campo numérico que indica la condicion de iva, según <a href="../tablas-de-referencia.md#condiciones-ante-el-iva">tabla de referencia Condiciones ante el IVA(**)</a>. Valores Permitidos: <strong>CF, RI, M, E </strong><br><strong>Ejemplo: RI</strong></p>                           |
| codigo               | Campo alfanumerico opcional. Longitud máxima 50 caracteres. **Ejemplo: Cobrado en ventanilla.**                                                                                                                                                                                            |

###

### Estructura de "Detalle de conceptos"

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

| `cantidad`              | <p>Campo numérico con 2 decimales. Separador de decimales: punto.<br><strong>Ejemplo: 1.50</strong></p>                                                                           |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `afecta_stock`          | <p>Campo alfanumérico de 1 posición. Valores posibles: "S" (si), "N" (no) <br><strong>Ejemplo: S</strong></p>                                                                     |
| `producto`              | Según estructura de producto                                                                                                                                                      |
| `leyenda`               | <p>Campo alfanumérico. Longitud máxima 100 caracteres. Contenido opcional. Será una descripción que acompañe al producto. <br><strong>Ejemplo: Blanca, cepillada</strong></p>     |
| bonificacion_porcentaje | Si se ha aplicado un porcentaje de descuento sobre éste concepto, debe ser enviado. Es un campo númerico con 2 decimales. El separador de decimales esperado es el punto. Ej:  25 |
|                         |                                                                                                                                                                                   |
|                         |                                                                                                                                                                                   |



### Estructura de "Concepto /  Producto"

{% hint style="info" %}
Si el producto ya existía en la base de datos de nuestra plataforma, para la lista de precios indicada basado en el código y/o descripción del mismo, será actualizado con los nuevos datos, solo si indicas que deseas actualizar el precio. En caso de no querer actualizar el producto, si el mismo ya existía, se facturará con el nuevo precio y descripción que envíes, pero mantendrá sus datos anteriores.
{% endhint %}

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

{% hint style="info" %}
Recuerda que las facturas C, no llevan IVA y debes enviar cada concepto con su precio final; sin embargo las facturas A y B deben enviarse siempre SIN IVA. Las facturas B llevan IVA siempre, solo que tu cliente no lo puede discriminar.
{% endhint %}

Los campos que debes enviar son los siguientes:

| `descripcion`                 | <p>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Papa blanca</strong></p>                                                                                                                                                                                                                                        |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `unidad_bulto`                | <p>Campo numérico entero requerido. Indica la cantidad de unidades que componen un bulto. Valor minimo esperado: 1<br><strong>Ejemplo: 12</strong></p>                                                                                                                                                                                     |
| `lista_precios`               | <p>Campo alfanumérico. Longitud máxima 255 caracteres. Nombre de la lista de precios a la cual pertenece. No saldrá impreso en la factura pero es requerido.<br><strong>Ejemplo: Verdura Orgánica</strong></p>                                                                                                                             |
| `codigo`                      | <p>Campo alfanumérico. Longitud máxima 10 caracteres. campo Opcional<br><strong>Ejemplo: ABX780</strong></p>                                                                                                                                                                                                                               |
| `precio_unitario_sin_iva`     | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                                                                                                                                                                                   |
| `alicuota`                    | <p>Indica la alicuota de IVA con la que grava ese producto. Valores Permitidos: </p><p><strong>27, 21 , 10.5 ,  0  ,  -1 ( para exento), -2 (no gravados)</strong><br><strong>Ejemplo: 10.5</strong></p>                                                                                                                                   |
| `unidad_medida`               | <p>Campo numérico que indica la unidad de medida, según<a href="../tablas-de-referencia.md#productos-unidades-de-medida-afip"> tabla de referencia Unidades de Medida(**). </a><br><strong>Ejemplo: 7</strong></p>                                                                                                                         |
| `actualiza_precio`            | Indica si se actualiza el precio del producto y sus datos adicionales como ser la unidad de medida, código, unidades por bulto y otros datos adicionales, en la base productos, tomando como valor de referencia el enviado en el comprobante. Campo Alfabético, de 1 caracter. Valores permitidos: S (si) N (no).          **Ejemplo: S** |
| `impuestos_internos_alicuota` | La alícuota que se cobra en concepto de impuestos internos para éste producto. Campo numerico, con  2 decimales.  ej: 10.5                                                                                                                                                                                                                 |
|                               |                                                                                                                                                                                                                                                                                                                                            |

{% hint style="info" %}
En caso que quieras reflejar en los comprobantes generados, un signo de porcentaje (%), deberás enviarlo en la descripción del producto de ésta manera:  **#\&#** , asi como si quisieras que parte de esa descripción del producto se imprima en otra linea, deberás enviar:  **#@# **
{% endhint %}

### Estructura de "Comprobantes Asociados" 

**Solo para las notas de débito y las notas de crédito**, AFIP requiere que se envíe un bloque de información adicional con "comprobantes asociados".  A partir del 01/04/2021 existen 2 maneras de informar los comprobantes asociados:

a) Detallando comprobantes asociados

b) Indicando un período de comprobantes asociados.

Podes ver un [ejemplo de comprobante con comprobantes asociados desde aquí](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-a-nota-de-debito-a-nota-de-credito-a)

{% hint style="info" %}
Solo deberán enviar los comprobantes asociados, cuando se emitan Notas de Débito o Notas de Crédito de tipo A, B, C, M y Comprobantes de tipo MiPyme.
{% endhint %}

#### a) Envío de comprobantes asociados detallados:

En caso de enviar el detalle de los comprobantes que se asocian, éstos deberán ser enviados dentro de un array, en el bloque  llamado "comprobantes_asociados", acorde a la estructura que se detalla a continuación para cada comprobante asociado.

A partir del 01/04/2021, y solo para comprobantes de tipo tradicional, AFIP habilitará una nueva herramienta para informar éstos comprobantes asociados, donde no se detallan enviar un periodo desde/hasta en lugar del detalle de cada comprobante asociado.Debes tener en cuenta que se excluyen de ésta modalidad de información,  los comprobantes de tipo exportación y MiPyme 

{% hint style="info" %}
En todos las notas de crédito y/o notas de débito de tipo MiPyme y/o de exportación,  **éste bloque es obligatorio.**
{% endhint %}

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

| `tipo_comprobante`  | Campo alfabético. Valores esperados según [tabla de tipos de comprobante.](../tablas-de-referencia.md#tipos-de-comprobantes)                                           |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `punto_venta`       | <p>Campo numérico entero. Longitud máxima 5 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                |
| `numero`            | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p> |
| `cuit`              | <p>Campo numérico, sin puntos ni guiones. Es el CUIT del emisor del comprobante asociado.<br><strong>Ejemplo: 1111111111</strong></p>                                  |
| `comprobante_fecha` | La fecha del comprobante en formato dd/mm/aaaa. El día y el mes deben tener 2 dígitos.                                                                                 |

#### b) Comprobantes asociados por período

Solo para comprobantes de tipo tradicional, y a partir del 01/04/2021, AFIP habilitará la posibilidad de emitir notas de débito y/o crédito indicando un período desde/hasta en lugar del detalle de comprobantes asociados. 

Para utilizar ésta herramienta,  **no se debe enviar el bloque** de "_comprobantes asociados"  _y en su lugar debe enviarse un bloque llamado_ "comprobantes_asociados_periodo", _el cual debe tener la siguiente estructura:

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

{% hint style="info" %}
Solo se podrá informar un periodo desde/hasta para aquellos comprobantes que **NO** sean de tipo: MiPyme ni comprobantes de exportación.
{% endhint %}

### Estructura de "RG Especiales" (solo según corresponda)

Según la RG a la que tu empresa aplique, se deberá enviar  un array con los datos adicionales, según se especifican en la [tabla de Datos adicionales para RG Especiales](../tablas-de-referencia.md#datos-opcionales-para-rg-especiales).

Ten en cuenta que solo podrás aplicar a un [regimen](../tablas-de-referencia.md#datos-opcionales-para-rg-especiales) por cada comprobante que emitas.

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

Información de los campos a enviar en el array de "datos":

| `id`    | Campo númerico. Valores esperados según [ ](../tablas-de-referencia.md#tipos-de-comprobantes)[Tabla de Datos Opcionales para RG Especiales](../tablas-de-referencia.md#datos-opcionales-para-rg-especiales) |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `valor` | Campo alfanumérico.                                                                                                                                                                                         |

{% hint style="info" %}
Ten en cuenta que TusFacturas NO realiza validaciones sobre éstos campos. Los realiza la propia AFIP en caso que corresponda.

Si uno de los items enviados posee el valor vacio, éste item no será procesado.
{% endhint %}

### Estructura de "pagos"  (opcional)

Si quisieras reflejar junto al envío del comprobante, el pago parcial o total del mismo, debes enviar un bloque, dentro del comprobante, llamado "pagos" con la estructura como se detalla a continuación.

Los pagos que informes, se usan solo para la gestión interna de nuestra plataforma y tu cliente no lo verá reflejado en el PDF del comprobante que emitiste, ya que el único objetivo que tiene éste bloque es nutrir la cuenta corriente de tu cliente, con el pago realizado.

{% hint style="info" %}
Cosas a tener en cuenta: 

* **NO** podrás enviar los siguientes medios de pago: cheques y detalle de retenciones.
* Se realizara una validación del total que se indique, contra la sumatoria de los medios de pago detallados
* El total de los pagos **NO** debe superar el importe total del comprobante, pero si puede ser inferior, para indicar que el comprobante recibió un pago parcial.
{% endhint %}

 Información de los campos que componen el **bloque "pagos"**

| nombre del campo | Requerido | Detalle                                                                                                  |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| formas_pago      | SI        | array con multiples items, según estructura que se detalla a continuación                                |
| total            | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p> |

Información de los campos que componen el **array de pagos > formas_pago **

| nombre del campo | Requerido | Detalle                                                                                                                                                                                 |
| ---------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| descripcion      | SI        | El nombre del medio de pago elegido para cancelar el comprobante. 255 caracteres max. En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente. |
| importe          | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                                |

Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
comprobante: {
   .... 
  			  "pagos" : {
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
