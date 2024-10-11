---
description: >-
  API AFIP para emitir comprobantes B. Ideal para Responsables Inscriptos.
  Ejemplos incluidos. Confiable desde 2015. ¡Los desarrolladores la aman!
---

# Ejemplos de comprobantes "B"

Los comprobantes de tipo "B" (Factura B / Notas de débito B / Nota de crédito B / Factura de crédito MiPyme B / Notas de crédito MiPyme B / Nota de débito MiPyme B), son aquellos que solo pueden ser emitidos por un CUIT cuya condición frente al IVA sea "Responsable inscripto" y se emitan a un consumidor final o un exento en IVA.&#x20;

No sabes en qué momento emitir comprobantes de tipo **B**? Consulta [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante B.&#x20;

### Ejemplo de Factura B

A continuación podrás ver un ejemplo del JSON para emitir una FACTURA B. Podes consultar la documentación con referencia a cada campo, [desde aquí](./).

<pre class="language-json"><code class="lang-json"><strong>{
</strong>   "apitoken":"xxxx",
   "usertoken":"xxxx",
   "apikey":"xxxx",
   "cliente":{
      "documento_tipo":"DNI",
      "condicion_iva":"CF",
      "domicilio":"Av Sta Fe 23132",
      "condicion_pago":"201",
      "documento_nro":"111132333",
      "razon_social":"Juan Pedro KJL",
      "provincia":"2",
      "email":"email@dominio.com",
      "envia_por_mail":"N",
       "rg5329": "N"
   },
   "comprobante":{
      "rubro":"Sevicios web",
      "tipo":"FACTURA B",
      "numero":2134,
      "bonificacion":0,
      "operacion":"V",
      "moneda":"PES",
      "cotizacion": 1,
      "detalle":[
         {
            "cantidad":1,
            "afecta_stock":"S",
            "actualiza_precio":"S",
            "bonificacion_porcentaje":0,
            "producto":{
               "descripcion":"Hosting pagina web ",
               "codigo":37,
               "lista_precios":"standard",
               "leyenda":"",
               "unidad_bulto":1,
               "alicuota":21,
               "actualiza_precio":"S",
               "rg5329": "N",
               "precio_unitario_sin_iva":114.88
            }
         }
      ],
      "fecha":"28/03/2018",
      "vencimiento":"26/03/2023",
      "rubro_grupo_contable":"Sevicios",
      "total":139.0,
      "cotizacion":1,
      "moneda":"PES",
      "punto_venta":3,
      "tributos":[]
   }
}
</code></pre>

#### ¿Cómo enviar una factura B según mi lenguaje de programación?

Podes enviar las facturas B por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos.

{% tabs %}
{% tab title="CURL" %}
```sh
curl --request POST
--url https://www.tusfacturas.app/app/api/v2/facturacion/nuevo
--header 'Content-Type: application/json'
--data '{ "apitoken":"xxxx", "cliente":{ "documento_tipo":"DNI", "condicion_iva":"CF", "domicilio":"Av Sta Fe 23132", "condicion_pago":"201", "documento_nro":"111132333", "razon_social":"Juan Pedro KJL", "provincia":"2", "email":"email@dominio.com", "envia_por_mail":"N", "rg5329": "N" }, "apikey":"xxxx", "comprobante":{ "rubro":"Sevicios web", "percepciones_iva":0, "tipo":"FACTURA B", "numero":2134, "bonificacion":0, "operacion":"V", "detalle":[ { "cantidad":1, "afecta_stock":"S", "actualiza_precio":"S", "bonificacion_porcentaje":0, "producto":{ "descripcion":"Hosting pagina web ", "codigo":37, "lista_precios":"standard", "leyenda":"", "unidad_bulto":1, "alicuota":21, "actualiza_precio":"S", "rg5329": "N", "precio_unitario_sin_iva":114.88 } } ], "fecha":"28/03/2018", "vencimiento":"26/03/2023", "rubro_grupo_contable":"Sevicios", "total":139.0, "cotizacion":1, "moneda":"PES", "punto_venta":3, "tributos":[] }, "usertoken":"xxxx" }'
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
  CURLOPT_POSTFIELDS => "{\n   \"apitoken\":\"xxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"DNI\",\n      \"condicion_iva\":\"CF\",\n      \"domicilio\":\"Av Sta Fe 23132\",\n      \"condicion_pago\":\"201\",\n      \"documento_nro\":\"111132333\",\n      \"razon_social\":\"Juan Pedro KJL\",\n      \"provincia\":\"2\",\n      \"email\":\"email@dominio.com\",\n      \"envia_por_mail\":\"N\",\n       \"rg5329\": \"N\"\n   },\n   \"apikey\":\"xxxx\",\n   \"comprobante\":{\n      \"rubro\":\"Sevicios web\",\n      \"percepciones_iva\":0,\n      \"tipo\":\"FACTURA B\",\n      \"numero\":2134,\n      \"bonificacion\":0,\n      \"operacion\":\"V\",\n      \"detalle\":[\n         {\n            \"cantidad\":1,\n            \"afecta_stock\":\"S\",\n            \"actualiza_precio\":\"S\",\n            \"bonificacion_porcentaje\":0,\n            \"producto\":{\n               \"descripcion\":\"Hosting pagina web \",\n               \"codigo\":37,\n               \"lista_precios\":\"standard\",\n               \"leyenda\":\"\",\n               \"unidad_bulto\":1,\n               \"alicuota\":21,\n               \"actualiza_precio\":\"S\",\n               \"rg5329\": \"N\",\n               \"precio_unitario_sin_iva\":114.88\n            }\n         }\n      ],\n      \"fecha\":\"28/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"rubro_grupo_contable\":\"Sevicios\",\n      \"total\":139.0,\n      \"cotizacion\":1,\n      \"moneda\":\"PES\",\n      \"punto_venta\":3,\n      \"tributos\":[]\n   },\n   \"usertoken\":\"xxxx\"\n}",
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

payload = "{\n   \"apitoken\":\"xxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"DNI\",\n      \"condicion_iva\":\"CF\",\n      \"domicilio\":\"Av Sta Fe 23132\",\n      \"condicion_pago\":\"201\",\n      \"documento_nro\":\"111132333\",\n      \"razon_social\":\"Juan Pedro KJL\",\n      \"provincia\":\"2\",\n      \"email\":\"email@dominio.com\",\n      \"envia_por_mail\":\"N\",\n       \"rg5329\": \"N\"\n   },\n   \"apikey\":\"xxxx\",\n   \"comprobante\":{\n      \"rubro\":\"Sevicios web\",\n      \"percepciones_iva\":0,\n      \"tipo\":\"FACTURA B\",\n      \"numero\":2134,\n      \"bonificacion\":0,\n      \"operacion\":\"V\",\n      \"detalle\":[\n         {\n            \"cantidad\":1,\n            \"afecta_stock\":\"S\",\n            \"actualiza_precio\":\"S\",\n            \"bonificacion_porcentaje\":0,\n            \"producto\":{\n               \"descripcion\":\"Hosting pagina web \",\n               \"codigo\":37,\n               \"lista_precios\":\"standard\",\n               \"leyenda\":\"\",\n               \"unidad_bulto\":1,\n               \"alicuota\":21,\n               \"actualiza_precio\":\"S\",\n               \"rg5329\": \"N\",\n               \"precio_unitario_sin_iva\":114.88\n            }\n         }\n      ],\n      \"fecha\":\"28/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"rubro_grupo_contable\":\"Sevicios\",\n      \"total\":139.0,\n      \"cotizacion\":1,\n      \"moneda\":\"PES\",\n      \"punto_venta\":3,\n      \"tributos\":[]\n   },\n   \"usertoken\":\"xxxx\"\n}"

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
const http = require("https");

const options = {
  "method": "POST",
  "hostname": "www.tusfacturas.app",
  "port": null,
  "path": "/app/api/v2/facturacion/nuevo",
  "headers": {
    "Content-Type": "application/json",
    "Content-Length": "1337"
  }
};

const req = http.request(options, function (res) {
  const chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function () {
    const body = Buffer.concat(chunks);
    console.log(body.toString());
  });
});

req.write(JSON.stringify({
  apitoken: 'xxxx',
  cliente: {
    documento_tipo: 'DNI',
    condicion_iva: 'CF',
    domicilio: 'Av Sta Fe 23132',
    condicion_pago: '201',
    documento_nro: '111132333',
    razon_social: 'Juan Pedro KJL',
    provincia: '2',
    email: 'email@dominio.com',
    envia_por_mail: 'N',
    rg5329: 'N'
  },
  apikey: 'xxxx',
  comprobante: {
    rubro: 'Sevicios web',
    percepciones_iva: 0,
    tipo: 'FACTURA B',
    numero: 2134,
    bonificacion: 0,
    operacion: 'V',
    detalle: [
      {
        cantidad: 1,
        afecta_stock: 'S',
        actualiza_precio: 'S',
        bonificacion_porcentaje: 0,
        producto: {
          descripcion: 'Hosting pagina web ',
          codigo: 37,
          lista_precios: 'standard',
          leyenda: '',
          unidad_bulto: 1,
          alicuota: 21,
          actualiza_precio: 'S',
          rg5329: 'N',
          precio_unitario_sin_iva: 114.88
        }
      }
    ],
    fecha: '28/03/2018',
    vencimiento: '26/03/2023',
    rubro_grupo_contable: 'Sevicios',
    total: 139,
    cotizacion: 1,
    moneda: 'PES',
    punto_venta: 3,
    tributos: []
  },
  usertoken: 'xxxx'
}));
req.end();
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
request.body = "{\n   \"apitoken\":\"xxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"DNI\",\n      \"condicion_iva\":\"CF\",\n      \"domicilio\":\"Av Sta Fe 23132\",\n      \"condicion_pago\":\"201\",\n      \"documento_nro\":\"111132333\",\n      \"razon_social\":\"Juan Pedro KJL\",\n      \"provincia\":\"2\",\n      \"email\":\"email@dominio.com\",\n      \"envia_por_mail\":\"N\",\n       \"rg5329\": \"N\"\n   },\n   \"apikey\":\"xxxx\",\n   \"comprobante\":{\n      \"rubro\":\"Sevicios web\",\n      \"percepciones_iva\":0,\n      \"tipo\":\"FACTURA B\",\n      \"numero\":2134,\n      \"bonificacion\":0,\n      \"operacion\":\"V\",\n      \"detalle\":[\n         {\n            \"cantidad\":1,\n            \"afecta_stock\":\"S\",\n            \"actualiza_precio\":\"S\",\n            \"bonificacion_porcentaje\":0,\n            \"producto\":{\n               \"descripcion\":\"Hosting pagina web \",\n               \"codigo\":37,\n               \"lista_precios\":\"standard\",\n               \"leyenda\":\"\",\n               \"unidad_bulto\":1,\n               \"alicuota\":21,\n               \"actualiza_precio\":\"S\",\n               \"rg5329\": \"N\",\n               \"precio_unitario_sin_iva\":114.88\n            }\n         }\n      ],\n      \"fecha\":\"28/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"rubro_grupo_contable\":\"Sevicios\",\n      \"total\":139.0,\n      \"cotizacion\":1,\n      \"moneda\":\"PES\",\n      \"punto_venta\":3,\n      \"tributos\":[]\n   },\n   \"usertoken\":\"xxxx\"\n}"

response = http.request(request)
puts response.read_body
```
{% endtab %}
{% endtabs %}

#### PDF de ejemplo de una Factura B

¿Necesitas una Factura B de ejemplo? [Descárgala ahora](https://www.tusfacturas.app/app/archivos-modelo/tipos-comprobante/27285051466\_\_FACTURA\_B-00010-00000167.pdf). Para personalizar el diseño, accede a nuestra [plataforma web](https://www.tusfacturas.app/app/login.html) >  Menú > Mi espacio de trabajo > CUITs/pDV > Editar.

#### Datos a tener en cuenta:

{% hint style="info" %}
* En los comprobantes B el IVA se suma al total del producto, pero no aparecerá desglozado en la factura, ya que tu cliente no lo puede discriminar. Vos debes enviarlo siempre SIN IVA el precio.
* ¿No sabes en qué momento emitir comprobantes de tipo B? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante B.&#x20;
* Si queres enviar un comprobante a un consumidor final, sin especificar su nombre y DNI, podes enviar:

&#x20;               Nro de documento = "0"

&#x20;              Tipo de documento = "OTRO"

&#x20;              En nombre, lo que tu contador/a te recomiende.

Tene en cuenta que ésto solo está permitido para comprobantes hasta ciertos montos. Consulta diariamente el monto actualizado por AFIP con el método de: [Consulta de topes CF](api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final.md)
{% endhint %}

***

### Notas de Crédito  B  - detallando los comprobantes que anulas.

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO B, que detalla los comprobantes asociados.

Podes consultar la documentación con referencia a cada campo, [desde aquí](api-factura-electronica-afip-notas-credito-debito.md).

```json
{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"DNI",
      "documento_nro":"12345678",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"CF"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"NOTA DE CREDITO B",
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
               "alicuota":"-1"
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
               "alicuota":"21"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         
      ],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":"112.1",
      "comprobantes_asociados":[
         {
            "tipo_comprobante":"FACTURA B",
            "punto_venta":"145",
            "numero":12313,
            "comprobante_fecha":"07/07/2018",
            "cuit":1111111111111
         }
      ]
   }
}
```

#### PDF de ejemplo de una Nota de crédito B

¿Necesitas una Nota de crédito B de ejemplo? [Descárgala ahora](https://www.tusfacturas.app/app/archivos-modelo/tipos-comprobante/27285051466\_\_NOTA\_DE\_CREDITO\_B-00010-00000005.pdf). Para personalizar el diseño, accede a nuestra [plataforma web](https://www.tusfacturas.app/app/login.html) >  Menú > Mi espacio de trabajo > CUITs/pDV > Editar.

***

### Nota de débito B - asociando períodos

A continuación podrás ver un ejemplo del JSON para emitir una Nota de débito B, que no detalla los comprobantes asociados, sino qué indica su período.

Podés consultar la documentación con referencia a cada campo [desde aquí](api-factura-electronica-afip-notas-credito-debito.md).

```json
{ "usertoken" :  "xxxxx", 
 "apikey"    :  "xxxx", 
 "apitoken"  :  "xxxxx",
 
"cliente": 
    {
         "documento_tipo":       "DNI", 
         "documento_nro":        "12345678", 
         "razon_social":         "VOUSYS TusFacturasAPP", 
         "email":                "a@a.com", 
         "domicilio":            "AV.LIBERTADOR 571", 
         "provincia":            "2", 
         "envia_por_mail":       "S", 
         "condicion_pago":       "211", 
         "condicion_iva":        "CF" 
    },
 
"comprobante": 
    {    "fecha":                    "20/03/2018", 
         "vencimiento":              "26/03/2023",
         "tipo":                     "NOTA DE DEBITO B", 
         "operacion":                "V", 
         "punto_venta":              "0002", 
         "numero":                   "00000012", 
         "moneda":"PES",
          "cotizacion": 1,
         "periodo_facturado_desde":  "28/02/2018", 
         "periodo_facturado_hasta":  "28/02/2018", 
         "rubro":                    "Alimentos", 
         "rubro_grupo_contable":     "Alimentos",

"detalle":
             [
                  {
                     "cantidad":     "1", 
                     "producto":     
                         {"descripcion":     "EXENTO - AVENA INSTANTANEA x5 kg. al 21", 
                         "unidad_bulto":     "1", 
                         "lista_precios":     "Lista de precios API 3", 
                         "codigo":     "16098", 
                         "precio_unitario_sin_iva":     "100",
                         "alicuota": "-1"
                         },
                     "leyenda":     ""
                 } ,

                  {
                     "cantidad":     "1", 
                     "producto":     
                         {"descripcion":     "p2", 
                         "unidad_bulto":     "1", 
                         "lista_precios":     "Lista de precios API 3", 
                         "codigo":     "160398", 
                         "precio_unitario_sin_iva":     "10",
                         "alicuota": "21"
                         },
                     "leyenda":     ""
                 }                  
  
             ],
         "bonificacion":             "0.00", 
         "leyenda_gral":             " ", 
         "tributos":                [],
         "impuestos_internos":       "0",
         "impuestos_internos_base":   "0",
         "impuestos_internos_alicuota": "0",
         "total":                    "112.1" ,
      "comprobantes_asociados_periodo": {
        "fecha_desde"   :    "20/11/2020",
        "fecha_hasta"  :    "25/11/2020" 
    } 
  } 
}

```



TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).
