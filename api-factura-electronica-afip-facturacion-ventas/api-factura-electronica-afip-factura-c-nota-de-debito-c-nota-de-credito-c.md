---
description: >-
  API AFIP para emitir comprobantes C. Ideal para Monotributistas. Ejemplos
  incluidos. Confiable desde 2015. ¡Los desarrolladores la aman!
---

# Ejemplos de comprobantes "C"

Los comprobantes de tipo "C" (Factura C / Nota de débito C / Nota de crédito C / Factura de crédito MiPyme C / Nota de crédito MiPyme C / Nota de débito MiPyme C), son aquellos que solo pueden ser emitidos por un CUIT cuya [condición frente al IVA](https://www.tusfacturas.app/que-tipo-de-comprobante-debo-emitir-segun-mi-condicion-frente-al-iva.html) sea "Monotributo" o "Exento".&#x20;

No sabes en qué momento emitir comprobantes de tipo **C**? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante C.&#x20;

### Ejemplo de Factura "C"

A continuación podrás ver un ejemplo del JSON para emitir una FACTURA C. Podes consultar la documentación con referencia a cada campo, [desde aquí](./).

```json
{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"FACTURA C",
      "operacion":"V",
      "punto_venta":"0002",
      "numero":"00000012",
      "moneda":"PES",
      "cotizacion": 1,
      "periodo_facturado_desde":"28/02/2018",
      "periodo_facturado_hasta":"28/02/2018",
      "rubro":"Alimentos",
      "rubro_grupo_contable":"Alimentos",
      "detalle":[
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"EXENTO - AVENA INSTANTANEA x5 kg. al 21",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"16098",
               "precio_unitario_sin_iva":"100",
               "alicuota":"0"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"p2",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"160398",
               "precio_unitario_sin_iva":"10",
               "alicuota":"0"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "total":"110" 
   }
}
```

### ¿Cómo enviar una factura C según mi lenguaje de programación?

Podes enviar las facturas C por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos.

{% tabs %}
{% tab title="CURL" %}
```sh
curl --request POST \
  --url https://www.tusfacturas.app/app/api/v2/facturacion/nuevo \
  --header 'Content-Type: application/json' \ 
  --data '{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"FACTURA C",
      "operacion":"V",
      "punto_venta":"0002",
      "moneda":"PES",
      "cotizacion": 1,
      "numero":"00000012",
      "periodo_facturado_desde":"28/02/2018",
      "periodo_facturado_hasta":"28/02/2018",
      "rubro":"Alimentos",
      "rubro_grupo_contable":"Alimentos",
      "detalle":[
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"EXENTO - AVENA INSTANTANEA x5 kg. al 21",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"16098",
               "precio_unitario_sin_iva":"100",
               "alicuota":"0"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"p2",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"160398",
               "precio_unitario_sin_iva":"10",
               "alicuota":"0"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "total":"110" 
   }
}'
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://www.tusfacturas.app/app/api/v2/facturacion/nuevo",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "{\n   \"usertoken\":\"xxxxx\",\n   \"apikey\":\"xxxx\",\n   \"apitoken\":\"xxxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"CUIT\",\n      \"documento_nro\":\"30712293841\",\n      \"razon_social\":\"VOUSYS TusFacturasAPP\",\n      \"email\":\"a@a.com\",\n      \"domicilio\":\"AV.LIBERTADOR 571\",\n      \"provincia\":\"2\",\n      \"envia_por_mail\":\"S\",\n      \"condicion_pago\":\"211\",\n      \"condicion_iva\":\"RI\"\n   },\n   \"comprobante\":{\n      \"fecha\":\"20/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"tipo\":\"FACTURA C\",\n      \"operacion\":\"V\",\n      \"punto_venta\":\"0002\",\n      \"numero\":\"00000012\",\n      \"periodo_facturado_desde\":\"28/02/2018\",\n      \"periodo_facturado_hasta\":\"28/02/2018\",\n      \"rubro\":\"Alimentos\",\n      \"rubro_grupo_contable\":\"Alimentos\",\n      \"detalle\":[\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"EXENTO - AVENA INSTANTANEA x5 kg. al 21\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"16098\",\n               \"precio_unitario_sin_iva\":\"100\",\n               \"alicuota\":\"0\"\n            },\n            \"leyenda\":\"\"\n         },\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"p2\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"160398\",\n               \"precio_unitario_sin_iva\":\"10\",\n               \"alicuota\":\"0\"\n            },\n            \"leyenda\":\"\"\n         }\n      ],\n      \"bonificacion\":\"0.00\",\n      \"leyenda_gral\":\" \",\n      \"total\":\"110\" \n   }\n}",
  CURLOPT_HTTPHEADER => [
    "Content-Type: application/json" 
  ],
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```
{% endtab %}

{% tab title="Python" %}
```python
import http.client

conn = http.client.HTTPSConnection("www.tusfacturas.app")

payload = "{\n   \"usertoken\":\"xxxxx\",\n   \"apikey\":\"xxxx\",\n   \"apitoken\":\"xxxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"CUIT\",\n      \"documento_nro\":\"30712293841\",\n      \"razon_social\":\"VOUSYS TusFacturasAPP\",\n      \"email\":\"a@a.com\",\n      \"domicilio\":\"AV.LIBERTADOR 571\",\n      \"provincia\":\"2\",\n      \"envia_por_mail\":\"S\",\n      \"condicion_pago\":\"211\",\n      \"condicion_iva\":\"RI\"\n   },\n   \"comprobante\":{\n      \"fecha\":\"20/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"tipo\":\"FACTURA C\",\n      \"operacion\":\"V\",\n      \"punto_venta\":\"0002\",\n      \"numero\":\"00000012\",\n      \"periodo_facturado_desde\":\"28/02/2018\",\n      \"periodo_facturado_hasta\":\"28/02/2018\",\n      \"rubro\":\"Alimentos\",\n      \"rubro_grupo_contable\":\"Alimentos\",\n      \"detalle\":[\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"EXENTO - AVENA INSTANTANEA x5 kg. al 21\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"16098\",\n               \"precio_unitario_sin_iva\":\"100\",\n               \"alicuota\":\"0\"\n            },\n            \"leyenda\":\"\"\n         },\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"p2\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"160398\",\n               \"precio_unitario_sin_iva\":\"10\",\n               \"alicuota\":\"0\"\n            },\n            \"leyenda\":\"\"\n         }\n      ],\n      \"bonificacion\":\"0.00\",\n      \"leyenda_gral\":\" \",\n      \"total\":\"110\" \n   }\n}"

headers = {
    'Content-Type': "application/json" 
    }

conn.request("POST", "/app/api/v2/facturacion/nuevo", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
var axios = require("axios").default;

var options = {
  method: 'POST',
  url: 'https://www.tusfacturas.app/app/api/v2/facturacion/nuevo',
  headers: {'Content-Type': 'application/json'},
  data: {
    usertoken: 'xxxxx',
    apikey: 'xxxx',
    apitoken: 'xxxxx',
    cliente: {
      documento_tipo: 'CUIT',
      documento_nro: '30712293841',
      razon_social: 'VOUSYS TusFacturasAPP',
      email: 'a@a.com',
      domicilio: 'AV.LIBERTADOR 571',
      provincia: '2',
      envia_por_mail: 'S',
      condicion_pago: '211',
      condicion_iva: 'RI'
    },
    comprobante: {
      fecha: '20/03/2018',
      vencimiento: '26/03/2023',
      tipo: 'FACTURA C',
      operacion: 'V',
      punto_venta: '0002',
      numero: '00000012',
      periodo_facturado_desde: '28/02/2018',
      periodo_facturado_hasta: '28/02/2018',
      rubro: 'Alimentos',
      rubro_grupo_contable: 'Alimentos',
      detalle: [
        {
          cantidad: '1',
          producto: {
            descripcion: 'EXENTO - AVENA INSTANTANEA x5 kg. al 21',
            unidad_bulto: '1',
            lista_precios: 'Lista de precios API 3',
            codigo: '16098',
            precio_unitario_sin_iva: '100',
            alicuota: '0'
          },
          leyenda: ''
        },
        {
          cantidad: '1',
          producto: {
            descripcion: 'p2',
            unidad_bulto: '1',
            lista_precios: 'Lista de precios API 3',
            codigo: '160398',
            precio_unitario_sin_iva: '10',
            alicuota: '0'
          },
          leyenda: ''
        }
      ],
      bonificacion: '0.00',
      leyenda_gral: ' ',
      total: '110'
    }
  }
};

axios.request(options).then(function (response) {
  console.log(response.data);
}).catch(function (error) {
  console.error(error);
});
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://www.tusfacturas.app/app/api/v2/facturacion/nuevo")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["Content-Type"] = 'application/json'
request.body = "{\n   \"usertoken\":\"xxxxx\",\n   \"apikey\":\"xxxx\",\n   \"apitoken\":\"xxxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"CUIT\",\n      \"documento_nro\":\"30712293841\",\n      \"razon_social\":\"VOUSYS TusFacturasAPP\",\n      \"email\":\"a@a.com\",\n      \"domicilio\":\"AV.LIBERTADOR 571\",\n      \"provincia\":\"2\",\n      \"envia_por_mail\":\"S\",\n      \"condicion_pago\":\"211\",\n      \"condicion_iva\":\"RI\"\n   },\n   \"comprobante\":{\n      \"fecha\":\"20/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"tipo\":\"FACTURA C\",\n      \"operacion\":\"V\",\n      \"punto_venta\":\"0002\",\n      \"numero\":\"00000012\",\n      \"periodo_facturado_desde\":\"28/02/2018\",\n      \"periodo_facturado_hasta\":\"28/02/2018\",\n      \"rubro\":\"Alimentos\",\n      \"rubro_grupo_contable\":\"Alimentos\",\n      \"detalle\":[\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"EXENTO - AVENA INSTANTANEA x5 kg. al 21\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"16098\",\n               \"precio_unitario_sin_iva\":\"100\",\n               \"alicuota\":\"0\"\n            },\n            \"leyenda\":\"\"\n         },\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"p2\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"160398\",\n               \"precio_unitario_sin_iva\":\"10\",\n               \"alicuota\":\"0\"\n            },\n            \"leyenda\":\"\"\n         }\n      ],\n      \"bonificacion\":\"0.00\",\n      \"leyenda_gral\":\" \",\n      \"total\":\"110\" \n   }\n}"

response = http.request(request)
puts response.read_body
```
{% endtab %}
{% endtabs %}

#### Datos a tener en cuenta:

{% hint style="info" %}
* Los comprobantes C no llevan IVA.
* No sabes en qué momento emitir comprobantes de tipo C? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante C.&#x20;
* Si querés enviar un comprobante a un consumidor final, sin especificar su nombre y DNI, podes enviar:

&#x20;               Nro de documento = "0"

&#x20;              Tipo de documento = "OTRO"

&#x20;              En nombre, lo que tu contador/a te recomiende.

Tene en cuenta que esto solo está permitido para comprobantes hasta ciertos montos. Consulta diariamente el monto actualizado por AFIP con el método de: [Consulta de topes CF](api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final.md)
{% endhint %}

#### PDF de ejemplo de una Factura C

¿Necesitas una Factura C de ejemplo? [Descárgala ahora](https://www.tusfacturas.app/app/archivos-modelo/tipos-comprobante/27285051466\_\_FACTURA\_C-00010-00000003.pdf). Para personalizar el diseño, accede a nuestra [plataforma web](https://www.tusfacturas.app/app/login.html) >  Menú > Mi espacio de trabajo > CUITs/pDV > Editar.

***

### NOTA DE CRÉDITO C

#### ¿Qué es una nota de crédito electrónica?

Es un comprobante dígital legalmente equivalente a la [nota de crédito](https://www.tusfacturas.app/como-emitir-notas-de-credito-electronica-afip.html) en formato papel, que la reemplaza en la mayoría de las operaciones de quienes estén obligados u opten por su utilización.

#### Ejemplo de: NOTA DE CRÉDITO C  - detallando los comprobantes que anulas.

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO C, que detalla los comprobantes asociados.

Podés consultar la documentación con referencia a cada campo, [desde aquí](api-factura-electronica-afip-notas-credito-debito.md).

```json
{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"NOTA DE CREDITO C",
      "moneda":"PES",
      "cotizacion": 1,
      "operacion":"V",
      "punto_venta":"0002",
      "numero":"00000012",
      "periodo_facturado_desde":"28/02/2018",
      "periodo_facturado_hasta":"28/02/2018",
      "rubro":"Alimentos",
      "rubro_grupo_contable":"Alimentos",
      "detalle":[
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"EXENTO - AVENA INSTANTANEA x5 kg. al 21",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"16098",
               "precio_unitario_sin_iva":"100",
               "alicuota":"0"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"p2",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"160398",
               "precio_unitario_sin_iva":"10",
               "alicuota":"0"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "total":"110",
      "comprobantes_asociados":[
         {
            "tipo_comprobante":"FACTURA C",
            "punto_venta":"145",
            "numero":12313,
            "comprobante_fecha":"07/07/2018",
            "cuit":1111111111111
         }
      ]
   }
}
```

#### PDF de ejemplo de una Nota de crédito C

¿Necesitas una Nota de crédito C de ejemplo? [Descárgala ahora](https://www.tusfacturas.app/app/archivos-modelo/tipos-comprobante/27285051466\_\_NOTA\_DE\_CREDITO\_C-00010-00000001.pdf). Para personalizar el diseño, accede a nuestra [plataforma web](https://www.tusfacturas.app/app/login.html) >  Menú > Mi espacio de trabajo > CUITs/pDV > Editar.&#x20;

***

### NOTA DE DÉBITO C&#x20;

#### ¿Qué es una nota de débito electrónica?

Es un comprobante dígital legalmente equivalente a la [nota de débito](https://www.tusfacturas.app/como-emitir-notas-de-debito-electronica-afip.html) en formato papel, que la reemplaza en la mayoría de las operaciones de quienes estén obligados u opten por su utilización.

#### Ejemplo de: NOTA DE DÉBITO C - asociando períodos

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE DEBITO C, que no detalla los comprobantes asociados, sino que indíca su período, tal como se especifica aquí.

Podés consultar la documentación con referencia a cada campo, [desde aquí.](api-factura-electronica-afip-notas-credito-debito.md)

```json
{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"NOTA DE DEBITO C",
      "operacion":"V",
      "punto_venta":"0002",
      "numero":"00000012",
      "moneda":"PES",
      "cotizacion": 1,
      "periodo_facturado_desde":"28/02/2018",
      "periodo_facturado_hasta":"28/02/2018",
      "rubro":"Alimentos",
      "rubro_grupo_contable":"Alimentos",
      "detalle":[
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"EXENTO - AVENA INSTANTANEA x5 kg. al 21",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"16098",
               "precio_unitario_sin_iva":"100",
               "alicuota":"0"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"p2",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"160398",
               "precio_unitario_sin_iva":"10",
               "alicuota":"0"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "total":"110",
      "comprobantes_asociados_periodo":{
         "fecha_desde":"20/11/2020",
         "fecha_hasta":"25/11/2020"
      }
   }
}
```



### Ejemplo de llamada en PHP

```php
// ENVIO REQUEST
$url ="https://www.tusfacturas.app/app/api/v2/facturacion/nuevo" ;
$ch = curl_init( $url );
curl_setopt( $ch, CURLOPT_POSTFIELDS,  json_encode ($facturacion_json) );
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

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).
