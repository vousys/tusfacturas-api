---
description: >-
  Emití con la API de TusFacturas.app los siguientes comprobantes: FACTURA E,
  NOTA DE DÉBITO E, NOTA DE CRÉDITO E.
---

# API - Factura electrónica AFIP | Comprobantes de tipo E (Factura de exportación)

A continuación te mostramos la estructura de los datos que se requieren para generar un comprobante de tipo exportación, ya sea NC, ND o FACTURA.

&#x20;Al final del documento encontrarás un ejemplo completo de comprobante de exportación.

## Estructura de datos campo "fex"

Para poder generar un [comprobante](./) de tipo E, se requiere enviar dentro del campo "**comprobante**", un campo adicional llamado: "**fex**", con la siguiente estructura :

```
{
        "permisos_tiene"      : "S" ,
        "fecha_pago"          : "12/10/2019",
        "tipo_exportacion"    : "2",
        "pais_comprobante_id" : "123",
        "forma_pago_leyenda"  : "Payment via paypal 30 days ",
        "cliente_pais_cuit"   : "50000000016",
        "incoterms_tipo_id"   : "FOB",
        "incoterms_nro"       : "AAAAGGGGGGGGGGGAAA ",
        "permisos"    : [
                            {
                                "codigo_despacho"  :  "1234567890123456",
                                 "pais_destino_id" :    "112"
                            },

                            {
                                "codigo_despacho"   :  "1234567890144456",
                                 "pais_destino_id"  :    "123"
                            },

                             {
                                "codigo_despacho"   :    "4444567890123456",
                                 "pais_destino_id"  :    "145"
                            }
                        ],
       "comprobantes_asociados": [
                            {
                                "tipo_comprobante"   :    "NOTA DE CREDITO E",
                                 "punto_venta"  :    "145",
                                 "numero"         : 12313,
                                 "comprobante_fecha": "07/07/2018",
                                 "cuit": 30111222334     
                            } 
                       ]
}
```

### Información de cada uno de los campos :

| `tipo_exportacion`       | <p>Campo numérico. Longitud 1 caracter. Valores esperados: <br>1= Exportación definitiva de bienes <br>2= Servicios <br>4= Otros. <br><strong>Ejemplo: 2</strong></p>                                                                                                                                                   |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `permisos_tiene`         | <p>Campo alfabético. Longitud 1 caracter. Indica si se posee documento aduanero de exportación (permiso de embarque). Valores esperados: <br>S= Si posee<br>N= No posee <br>(vacio)= No especifica <br><strong>Ejemplo: S</strong></p>                                                                                  |
| `permisos`               | Solo deberán ser enviados los permisos cuando el campo permisos\_tiene sea igual a "S".    Valores a enviar según estructura de datos definida en  ["Permisos de exportacion".](api-factura-electronica-afip-factura-electronica-afip-exportacion.md#estructura-de-permisos)                                             |
| `pais_comprobante_id`    | <p>Campo numérico. Según tabla de referencia <a href="../consulta-de-paises-afip.md">Paises AFIP (**)</a> <br><strong>Ejemplo: 123</strong></p>                                                                                                                                                                          |
| `forma_pago_leyenda`     | <p>Campo alfanumérico. Descripción adicional de la forma de pago <br><strong>Ejemplo: Favor depositar en cuenta XXXXX</strong></p>                                                                                                                                                                                      |
| `cliente_pais_cuit`      | <p>Campo numérico. Según tabla de referencia <a href="../consulta-de-cuit-pais-afip.md">CUIT Pais AFIP (**) </a><br><strong>Ejemplo: 51600004380</strong></p>                                                                                                                                                            |
| `incoterms_tipo_id`      | <p>Campo alfabético Incoterms – Cláusula de Venta. Según tabla de referencia <a href="../consulta-de-incoterms.md">Incoterms (**) </a><br><strong>Ejemplo: EXW</strong></p>                                                                                                                                             |
| `incoterms_nro`          | <p>Campo alfanumérico - Información complementaria del incoterm <br><strong>Ejemplo: Texto dic.</strong></p>                                                                                                                                                                                                            |
| `comprobantes_asociados` | Se deberá informar el/los comprobante/s asociados solamente si el comprobante que se está autorizando corresponde a una Nota de Débito o Nota de Crédito. Según estructura de "[Comprobantes asociados"](api-factura-electronica-afip-factura-electronica-afip-exportacion.md#estructura-de-comprobantes-asociados). |
| fecha\_pago              | Campo fecha - formato esperado: dd/mm/aaaa. Éste campo es obligatorio únicamente para Facturas E, si se envia tipo\_exportacion = 2 o tipo\_exportacion=4                                                                                                                                                                |

### Estructura de "Permisos "

Cada uno de los permisos de exportación que disponga, deberán ser enviados acordes a la estructura que se detalla a continuación

```
{
 "codigo_despacho"  :  "1234567890123456",
 "pais_destino_id" :    "112"
}
```

Información de los campos a enviar:Información de los campos a enviar:

| `codigo_despacho` | Campo alfanumérico. Longitud 16 caracteres. Deberá ser un permiso válido, formato 99999AAXX999999A (donde XX podrán ser números o letras).  |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `pais_destino_id` | <p>Campo numérico. Según tabla de referencia <a href="../consulta-de-paises-afip.md">Paises AFIP (**)</a> <br><strong>Ejemplo: 123</strong></p> |

### Estructura de "Comprobantes Asociados"

Cada uno de los comprobantes asociados de exportación que disponga, deberán ser enviados acordes a la estructura que se detalla a continuación.

{% hint style="info" %}
Solo deberán ser enviados los comprobantes asociados, cuando el campo exportacion\_tipo sea igual a "1" .
{% endhint %}

```
 {
    "tipo_comprobante"   :    "NOTA DE CREDITO E",
     "punto_venta"  :    "145",
     "numero" : 12313,
     "cuit": 30111222334     
} 
```

Solo deberán ser enviados los comprobantes asociados, cuando el campo exportacion\_tipo sea igual a "1"

Información de los campos a enviar:

| `tipo_comprobante` | Campo alfabético. Valores esperados: "FACTURA E", "NOTA DE DEBITO E", "NOTA DE CREDITO E"                                                                              |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `punto_venta`      | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                |
| `numero`           | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p> |
| `CUIT`             | <p>Campo numérico, sin puntos ni guiones.<br><strong>Ejemplo: 30111222334</strong></p>                                                                                 |

## Ejemplo de JSON completo a enviar&#x20;

{% hint style="info" %}
Para comprobantes de tipo E, los siguientes campos deberá enviarlos en cero:  bonificación, exentos, percepciones (IIBB e IVA), no gravados, impuestos internos.
{% endhint %}

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
                    "condicion_pago":       "30",
                    "condicion_iva":        "CF"
                },
"comprobante":  {
                "fecha":                    "28\/07\/2015",
                "tipo":                     "NOTA DE DEBITO E",
                "moneda":                   "DOL",
               "idioma":                   "1",
                "cotizacion":               "15.20",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6",
                "periodo_facturado_desde":  "27\/07\/2015",
                "periodo_facturado_hasta":  "30\/07\/2015",
                "rubro":                    "Servicios web",
                "rubro_grupo_contable":     "servicios",
                "fex": {
                            "permisos_tiene"      : "S" ,
                            "tipo_exportacion"    : "1",
                            "pais_comprobante_id" : "123",
                            "forma_pago_leyenda"  : "Payment via paypal 30 days ",
                            "cliente_pais_cuit"   : "50000000016",
                            "incoterms_tipo_id"   : "FOB",
                            "incoterms_nro"       : "AAAAGGGGGGGGGGGAAA ",
                            "permisos"    : [
                                                {
                                                    "codigo_despacho"  :  "1234567890123456",
                                                     "pais_destino_id" :    "112"
                                                },
                    
                                                {
                                                    "codigo_despacho"   :  "1234567890144456",
                                                     "pais_destino_id"  :    "123"
                                                },
                    
                                                 {
                                                    "codigo_despacho"   :    "4444567890123456",
                                                     "pais_destino_id"  :    "145"
                                                }
                                            ],
                           "comprobantes_asociados": [
                                                {
                                                    "tipo_comprobante"   :    "NOTA DE CREDITO E",
                                                     "punto_venta"  :    "145",
                                                     "numero" : 12313,
                                                     "cuit": 30111222334     
                                                } 
                                           ]
                    },
                "detalle":
                            [
                                {
                                    "cantidad":"1",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "PAPAS",
                                             "unidad_bulto":    "10",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "",
                                             "precio_unitario_sin_iva":"100.45",
                                             "alicuota":      "21",
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":"blanca, cepillada"
                                },
                                {
                                    "cantidad":"1.5",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "HUEVOS",
                                             "unidad_bulto":    "30",
                                             "lista_precios":   "MAPPLETS",
                                             "codigo":          "MPH",
                                             "precio_unitario_sin_iva":"50",
                                             "alicuota":      "10.5",
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":""
                                },
                                {
                                    "cantidad":"2",
                                    "afecta_stock": "S",
                                    "producto":
                                            {"descripcion":     "ZANAHORIA",
                                             "unidad_bulto":    "50",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "ZNH1",
                                             "precio_unitario_sin_iva":"200",
                                             "alicuota":      "21",
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":""
                                }
                            ],
                "bonificacion":             "0",
                "leyenda_gral":             "bla bla bla",
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
                "total":                    "575.45"
        }
}

```

### Ejemplo de llamada en PHP

```
// ENVIO REQUEST
$url ="https://www.tusfacturas.app/app/api/v2/facturacion/nuevo" ;
$ch = curl_init( $url );
curl_setopt( $ch, CURLOPT_POSTFIELDS,  json_encode($data) );
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
$json_rta_curl =  json_decode(  curl_exec($ch) ) ;  
curl_close($ch);

// MUESTRO RESPUESTA
echo "<p>MENSAJE:". $json_rta_curl->rta."</p>"; 
echo "<p>Vencimiento del pago:".$json_rta_curl->vencimiento_pago."</p>"; 
echo "<p>CAE:".$json_rta_curl->cae."</p>"; 
echo "<p>Vencimiento del cae:".$json_rta_curl->vencimiento_cae."</p>"; 
echo "<p>Comprobante pdf url:".$json_rta_curl->comprobante_pdf_url."</p>"; 
echo "<p>error:". $json_rta_curl->error ."</p>"; 
echo "<p>errores:". implode("," , $json_rta_curl->errores) ."</p>"; 


```
