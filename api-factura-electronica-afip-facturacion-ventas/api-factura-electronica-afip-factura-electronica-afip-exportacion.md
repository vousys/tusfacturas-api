---
description: >-
  Emití con la API de TusFacturas.app los siguientes comprobantes: FACTURA E,
  NOTA DE DÉBITO E, NOTA DE CRÉDITO E.
---

# Comprobantes de exportación de tipo "E"

TusFacturasAPP es un proveedor SaaS líder de servicios de facturación electrónica en Argentina, que permite a empresas de todos los tamaños emitir comprobantes fiscales válidos de manera rápida, segura y cumpliendo con todas las regulaciones de la AFIP.

### ¿Qué podes hacer con la API para facturación AFIP?

Integra fácilmente la facturación electrónica en tu software con la API de TusFacturasAPP. Emite comprobantes fiscales válidos desde tu sistema y obtén respuestas inmediatas de la AFIP.

<figure><img src="../.gitbook/assets/157.webp" alt="SDK AFIP. TusFacturasAPP API Factura Electronica AFIP. AFIP WS"><figcaption></figcaption></figure>

### ¿Cómo empiezo?

Te sugerimos revisar la guia de [¿Cómo empiezo?](../como-empiezo.md) . Una vez configurada tu cuenta y creado tu CUIT+Punto de venta (PDV) en [TusFacturasAPP](https://www.tusfacturas.app), podrás comenzar a emitir facturas electrónicas AFIP Argentina válidas.&#x20;

Comenza ya a cumplir con las regulaciones fiscales y brinda una experiencia de facturación digital eficiente a tus clientes. [Solicita acceso](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html) a nuestra API de facturación electrónica.A continuación te mostramos la estructura de los datos que se requieren para generar un comprobante de tipo exportación, ya sea NC, ND o FACTURA.

### ¿Cómo crear una Comprobantes de exportacion "E"**?**

Consulta nuestra guía detallada "[API Facturación AFIP](./)" para conocer a profundidad el servicio, los requerimientos de cada solicitud y los datos específicos que debes enviar para generar nuevos comprobantes de venta. Nuestra documentación completa y ejemplos de código te facilitarán una integración rápida y eficiente de la facturación electrónica en tu sistema actual.

Para emitir un comprobante de tipo "E" se requiere agregar el bloque "fex" al request que armes. A continuación podrás ver ejemplos y su estructura.

### Estructura de datos bloque: "fex"

Para poder generar un [comprobante](./) de tipo E, se requiere enviar dentro del campo "**comprobante**", un campo adicional llamado: "**fex**", con la siguiente estructura :

#### Ejemplo de JSON para FACTURA E

```
{ 

  "comprobante": { 
        ..., 
        "fex": {
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
                              ]
               
      }
}
```

### Información de cada uno de los campos :

| `tipo_exportacion`       | <p>Campo numérico. Longitud 1 caracter. Valores esperados:<br>1= Exportación definitiva de bienes<br>2= Servicios<br>4= Otros.<br><strong>Ejemplo: 2</strong></p>                                                                                                                                                                 |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `permisos_tiene`         | <p>Campo alfabético. Longitud 1 caracter. Indica si se posee documento aduanero de exportación (permiso de embarque). Valores esperados:<br>S= Si posee<br>N= No posee<br>(vacio)= No especifica<br><strong>Ejemplo: S</strong></p>                                                                                               |
| `permisos`               | Solo deberán ser enviados los permisos cuando el campo permisos\_tiene sea igual a "S". Valores a enviar según estructura de datos definida en ["Permisos de exportacion".](api-factura-electronica-afip-factura-electronica-afip-exportacion.md#estructura-de-permisos)                                                           |
| `pais_comprobante_id`    | <p>Campo numérico. Según tabla de referencia <a href="../parametros/consulta-de-paises-afip.md">Paises AFIP (**)</a><br><strong>Ejemplo: 123</strong></p>                                                                                                                                                                          |
| `forma_pago_leyenda`     | <p>Campo alfanumérico. Descripción adicional de la forma de pago<br><strong>Ejemplo: Favor depositar en cuenta XXXXX</strong></p>                                                                                                                                                                                                 |
| `cliente_pais_cuit`      | <p>Campo numérico. Según tabla de referencia <a href="../parametros/consulta-de-cuit-pais-afip.md">CUIT Pais AFIP (**)</a><br><strong>Ejemplo: 51600004380</strong></p>                                                                                                                                                            |
| `incoterms_tipo_id`      | <p>Campo alfabético Incoterms – Cláusula de Venta. Según tabla de referencia <a href="../parametros/consulta-de-incoterms.md">Incoterms (**)</a><br><strong>Ejemplo: EXW</strong></p>                                                                                                                                             |
| `incoterms_nro`          | <p>Campo alfanumérico - Información complementaria del incoterm<br><strong>Ejemplo: Texto dic.</strong></p>                                                                                                                                                                                                                       |
| `comprobantes_asociados` | OPCIONAL. Se deberá informar el/los comprobante/s asociados solamente si el comprobante que se está autorizando corresponde a una Nota de Débito o Nota de Crédito. Según estructura de "[Comprobantes asociados"](api-factura-electronica-afip-factura-electronica-afip-exportacion.md#estructura-de-comprobantes-asociados). |
| fecha\_pago              | Campo fecha - formato esperado: dd/mm/aaaa. Éste campo es obligatorio únicamente para Facturas E, si se envia tipo\_exportacion = 2 o tipo\_exportacion=4                                                                                                                                                                          |

### Estructura de "Permisos "

Cada uno de los permisos de exportación que disponga, deberán ser enviados acordes a la estructura que se detalla a continuación

```
{
 "codigo_despacho"  :  "1234567890123456",
 "pais_destino_id" :    "112"
}
```

Información de los campos a enviar:Información de los campos a enviar:

| `codigo_despacho` | Campo alfanumérico. Longitud 16 caracteres. Deberá ser un permiso válido, formato 99999AAXX999999A (donde XX podrán ser números o letras).            |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pais_destino_id` | <p>Campo numérico. Según tabla de referencia <a href="../parametros/consulta-de-paises-afip.md">Paises AFIP (**)</a><br><strong>Ejemplo: 123</strong></p> |

{% hint style="info" %}
Datos a tener en cuenta para los comprobantes de exportación:&#x20;

Los siguientes campos dentro del json del comprobante deberá enviarlos en cero:&#x20;

* bonificación,&#x20;
* no gravados&#x20;
* impuestos internos.

El bloque tributos deberá ser enviado vacío.
{% endhint %}

### Notas de crédito E / Notas de débito E

En caso que debas anular una factura de exportación, el comprobante que debes emitir es una Nota de crédito E, para ésto debes agregar dentro del bloque "fex" un bloque adicional según estructura de "[comprobantes\_asociados](api-factura-electronica-afip-notas-credito-debito.md#ejemplos-json-completos)", que es un array con cada uno de los comprobantes de tipo E que se quieren anular contablemente. Te sugerimos consultar la documentación de [Notas de crédito / Notas de débit](api-factura-electronica-afip-notas-credito-debito.md)o para conocer como el bloque que debes enviar.

{% hint style="info" %}
Solo deberán ser enviados los comprobantes asociados, cuando el campo exportacion\_tipo sea igual a "1" .
{% endhint %}



### Ejemplo de NOTA DE DÉBITO E

```json
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"cliente"   :
                {   
                .....
                },
"comprobante":  {
                ....,
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
                "detalle": [
                          .... ]
        }
}
```

### Ejemplo de llamada en PHP

```php
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
