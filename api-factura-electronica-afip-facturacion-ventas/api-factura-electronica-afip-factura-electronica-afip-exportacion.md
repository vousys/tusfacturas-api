---
description: >-
  API de facturación electrónica AFIP para emitir comprobantes de exportación de
  tipo E: FACTURA E, NOTA DE DÉBITO E, NOTA DE CRÉDITO E.
---

# Comprobantes de exportación de tipo "E"

TusFacturasAPP es un proveedor SaaS líder de servicios de facturación electrónica en Argentina, que permite a empresas de todos los tamaños emitir comprobantes fiscales válidos de manera rápida, segura y cumpliendo con todas las regulaciones de la AFIP.

### ¿Qué podes hacer con la API para facturación AFIP?

Integra fácilmente la facturación electrónica en tu software con la API de TusFacturasAPP. Emite comprobantes fiscales válidos desde tu sistema y obtén respuestas inmediatas de la AFIP.

<figure><img src="../.gitbook/assets/157.webp" alt="SDK AFIP. TusFacturasAPP API Factura Electronica AFIP. AFIP WS"><figcaption></figcaption></figure>

### ¿Cómo empiezo?

Te sugerimos revisar la guia de [¿Cómo empiezo?](../como-empiezo.md) . Una vez configurada tu cuenta y creado tu CUIT+Punto de venta (PDV) en [TusFacturasAPP](https://www.tusfacturas.app), podrás comenzar a emitir facturas electrónicas AFIP Argentina válidas.&#x20;

Comenza ya a cumplir con las regulaciones fiscales y brinda una experiencia de facturación digital eficiente a tus clientes. [Solicita acceso](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html) a nuestra API de facturación electrónica.A continuación te mostramos la estructura de los datos que se requieren para generar un comprobante de tipo exportación, ya sea NC, ND o FACTURA.

### ¿Qué son las **Facturas Electrónicas de Exportación "E"?**

Las **Facturas Electrónicas de Exportación "E"** son comprobantes digitales que respaldan las ventas de bienes o servicios realizados a clientes en el exterior. Son emitidas de forma obligatoria por empresas argentinas que realizan operaciones de exportación.

### **¿Qué las diferencia de las facturas electrónicas comunes?**

* **Uso específico:** Las Facturas "E" se utilizan exclusivamente para **ventas a compradores no residentes en el país**.
* **Información adicional:** Las Facturas "E" requieren datos específicos relacionados con la exportación, como el **destino de la mercadería**, el **medio de transporte** y los **datos del comprador extranjero**.
* **Exención de IVA:** Las exportaciones de bienes y servicios generalmente están exentas del IVA, lo que se refleja en las Facturas "E".

### **¿Quiénes deben emitir Facturas "E"?**

Están obligadas a emitir Facturas "E" todas las empresas argentinas que realicen:

* **Ventas de bienes al exterior:** Incluye productos físicos, como mercaderías, maquinaria y alimentos.
* **Prestaciones de servicios a no residentes:** Abarca servicios como consultoría, turismo, transporte internacional y otros.

### **¿Cómo emitir Facturas "E"?**

La emisión de Facturas "E" se realiza de forma electrónica a través de **AFIP** o mediante **software homologado por la AFIP, como lo es**[ **TusFacturas.app**](https://www.tusfacturas.app).

### ¿Cómo crear una Comprobantes de exportacion "E"**?**

**En esta guía encontrarás:**

* **Explicación detallada del servicio  en nuestra guia:** [**API Facturación AFIP**](./)**.**
* **Requerimientos específicos para cada tipo de solicitud.**
* **Datos exactos para generar nuevos comprobantes de venta.**
* **Documentación completa y ejemplos de código para una integración rápida y eficiente.**

#### **Emisión simplificada de Comprobantes "E":**

Para emitir Comprobantes Electrónicos de Exportación ("E"), solo debes **agregar el bloque "fex" al request** que construyas, con la siguiente estructura :

#### Ejemplo de JSON para FACTURA E

```json
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

### ¿Cómo enviar una factura E según mi lenguaje de programación?

Podes enviar las facturas E por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos.

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
      "condicion_iva":"RI",
      "rg5329":"N"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"FACTURA E",
      "operacion":"V",
      "moneda":"DOL",
      "cotizacion": 1234.55,
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
               "alicuota":"-1",
               "rg5329":"N"
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
               "alicuota":"21",
               "rg5329":"N"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         {
            "tipo":6,
            "regimen":2,
            "base_imponible":100,
            "alicuota":10,
            "total":10
         },
         {
            "tipo":7,
            "regimen":5,
            "base_imponible":200,
            "alicuota":10,
            "total":20
         }
      ],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":"142.1",
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
  CURLOPT_POSTFIELDS => "{\n   \"usertoken\":\"xxxxx\",\n   \"apikey\":\"xxxx\",\n   \"apitoken\":\"xxxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"CUIT\",\n      \"documento_nro\":\"30712293841\",\n      \"razon_social\":\"VOUSYS TusFacturasAPP\",\n      \"email\":\"a@a.com\",\n      \"domicilio\":\"AV.LIBERTADOR 571\",\n      \"provincia\":\"2\",\n      \"envia_por_mail\":\"S\",\n      \"condicion_pago\":\"211\",\n      \"condicion_iva\":\"RI\",\n      \"rg5329\":\"N\"\n   },\n   \"comprobante\":{\n      \"fecha\":\"20/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"tipo\":\"FACTURA E\",\n      \"operacion\":\"V\",\n      \"punto_venta\":\"0002\",\n      \"numero\":\"00000012\",\n      \"periodo_facturado_desde\":\"28/02/2018\",\n      \"periodo_facturado_hasta\":\"28/02/2018\",\n      \"rubro\":\"Alimentos\",\n      \"rubro_grupo_contable\":\"Alimentos\",\n      \"detalle\":[\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"EXENTO - AVENA INSTANTANEA x5 kg. al 21\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"16098\",\n               \"precio_unitario_sin_iva\":\"100\",\n               \"alicuota\":\"-1\",\n               \"rg5329\":\"N\"\n            },\n            \"leyenda\":\"\"\n         },\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"p2\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"160398\",\n               \"precio_unitario_sin_iva\":\"10\",\n               \"alicuota\":\"21\",\n               \"rg5329\":\"N\"\n            },\n            \"leyenda\":\"\"\n         }\n      ],\n      \"bonificacion\":\"0.00\",\n      \"leyenda_gral\":\" \",\n      \"tributos\":[\n         {\n            \"tipo\":6,\n            \"regimen\":2,\n            \"base_imponible\":100,\n            \"alicuota\":10,\n            \"total\":10\n         },\n         {\n            \"tipo\":7,\n            \"regimen\":5,\n            \"base_imponible\":200,\n            \"alicuota\":10,\n            \"total\":20\n         }\n      ],\n      \"impuestos_internos\":\"0\",\n      \"impuestos_internos_base\":\"0\",\n      \"impuestos_internos_alicuota\":\"0\",\n      \"total\":\"142.1\",\n\t\t \"fex\": {\n              \"permisos_tiene\"      : \"S\" ,\n              \"fecha_pago\"          : \"12/10/2019\",\n              \"tipo_exportacion\"    : \"2\",\n              \"pais_comprobante_id\" : \"123\",\n              \"forma_pago_leyenda\"  : \"Payment via paypal 30 days \",\n              \"cliente_pais_cuit\"   : \"50000000016\",\n              \"incoterms_tipo_id\"   : \"FOB\",\n              \"incoterms_nro\"       : \"AAAAGGGGGGGGGGGAAA \",\n              \"permisos\"    : [\n                                  {\n                                      \"codigo_despacho\"  :  \"1234567890123456\",\n                                       \"pais_destino_id\" :    \"112\"\n                                  },\n\n                                  {\n                                      \"codigo_despacho\"   :  \"1234567890144456\",\n                                       \"pais_destino_id\"  :    \"123\"\n                                  },\n                                   {\n                                      \"codigo_despacho\"   :    \"4444567890123456\",\n                                       \"pais_destino_id\"  :    \"145\"\n                                  }\n                              ]\n               \n      }\n\t\t \n   }\n}",
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

payload = "{\n   \"usertoken\":\"xxxxx\",\n   \"apikey\":\"xxxx\",\n   \"apitoken\":\"xxxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"CUIT\",\n      \"documento_nro\":\"30712293841\",\n      \"razon_social\":\"VOUSYS TusFacturasAPP\",\n      \"email\":\"a@a.com\",\n      \"domicilio\":\"AV.LIBERTADOR 571\",\n      \"provincia\":\"2\",\n      \"envia_por_mail\":\"S\",\n      \"condicion_pago\":\"211\",\n      \"condicion_iva\":\"RI\",\n      \"rg5329\":\"N\"\n   },\n   \"comprobante\":{\n      \"fecha\":\"20/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"tipo\":\"FACTURA E\",\n      \"operacion\":\"V\",\n      \"punto_venta\":\"0002\",\n      \"numero\":\"00000012\",\n      \"periodo_facturado_desde\":\"28/02/2018\",\n      \"periodo_facturado_hasta\":\"28/02/2018\",\n      \"rubro\":\"Alimentos\",\n      \"rubro_grupo_contable\":\"Alimentos\",\n      \"detalle\":[\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"EXENTO - AVENA INSTANTANEA x5 kg. al 21\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"16098\",\n               \"precio_unitario_sin_iva\":\"100\",\n               \"alicuota\":\"-1\",\n               \"rg5329\":\"N\"\n            },\n            \"leyenda\":\"\"\n         },\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"p2\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"160398\",\n               \"precio_unitario_sin_iva\":\"10\",\n               \"alicuota\":\"21\",\n               \"rg5329\":\"N\"\n            },\n            \"leyenda\":\"\"\n         }\n      ],\n      \"bonificacion\":\"0.00\",\n      \"leyenda_gral\":\" \",\n      \"tributos\":[\n         {\n            \"tipo\":6,\n            \"regimen\":2,\n            \"base_imponible\":100,\n            \"alicuota\":10,\n            \"total\":10\n         },\n         {\n            \"tipo\":7,\n            \"regimen\":5,\n            \"base_imponible\":200,\n            \"alicuota\":10,\n            \"total\":20\n         }\n      ],\n      \"impuestos_internos\":\"0\",\n      \"impuestos_internos_base\":\"0\",\n      \"impuestos_internos_alicuota\":\"0\",\n      \"total\":\"142.1\",\n\t\t \"fex\": {\n              \"permisos_tiene\"      : \"S\" ,\n              \"fecha_pago\"          : \"12/10/2019\",\n              \"tipo_exportacion\"    : \"2\",\n              \"pais_comprobante_id\" : \"123\",\n              \"forma_pago_leyenda\"  : \"Payment via paypal 30 days \",\n              \"cliente_pais_cuit\"   : \"50000000016\",\n              \"incoterms_tipo_id\"   : \"FOB\",\n              \"incoterms_nro\"       : \"AAAAGGGGGGGGGGGAAA \",\n              \"permisos\"    : [\n                                  {\n                                      \"codigo_despacho\"  :  \"1234567890123456\",\n                                       \"pais_destino_id\" :    \"112\"\n                                  },\n\n                                  {\n                                      \"codigo_despacho\"   :  \"1234567890144456\",\n                                       \"pais_destino_id\"  :    \"123\"\n                                  },\n                                   {\n                                      \"codigo_despacho\"   :    \"4444567890123456\",\n                                       \"pais_destino_id\"  :    \"145\"\n                                  }\n                              ]\n               \n      }\n\t\t \n   }\n}"

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
  headers: {'Content-Type': 'application/json',
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
      condicion_iva: 'RI',
      rg5329: 'N'
    },
    comprobante: {
      fecha: '20/03/2018',
      vencimiento: '26/03/2023',
      tipo: 'FACTURA E',
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
            alicuota: '-1',
            rg5329: 'N'
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
            alicuota: '21',
            rg5329: 'N'
          },
          leyenda: ''
        }
      ],
      bonificacion: '0.00',
      leyenda_gral: ' ',
      tributos: [
        {tipo: 6, regimen: 2, base_imponible: 100, alicuota: 10, total: 10},
        {tipo: 7, regimen: 5, base_imponible: 200, alicuota: 10, total: 20}
      ],
      impuestos_internos: '0',
      impuestos_internos_base: '0',
      impuestos_internos_alicuota: '0',
      total: '142.1',
      fex: {
        permisos_tiene: 'S',
        fecha_pago: '12/10/2019',
        tipo_exportacion: '2',
        pais_comprobante_id: '123',
        forma_pago_leyenda: 'Payment via paypal 30 days ',
        cliente_pais_cuit: '50000000016',
        incoterms_tipo_id: 'FOB',
        incoterms_nro: 'AAAAGGGGGGGGGGGAAA ',
        permisos: [
          {codigo_despacho: '1234567890123456', pais_destino_id: '112'},
          {codigo_despacho: '1234567890144456', pais_destino_id: '123'},
          {codigo_despacho: '4444567890123456', pais_destino_id: '145'}
        ]
      }
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
request.body = "{\n   \"usertoken\":\"xxxxx\",\n   \"apikey\":\"xxxx\",\n   \"apitoken\":\"xxxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"CUIT\",\n      \"documento_nro\":\"30712293841\",\n      \"razon_social\":\"VOUSYS TusFacturasAPP\",\n      \"email\":\"a@a.com\",\n      \"domicilio\":\"AV.LIBERTADOR 571\",\n      \"provincia\":\"2\",\n      \"envia_por_mail\":\"S\",\n      \"condicion_pago\":\"211\",\n      \"condicion_iva\":\"RI\",\n      \"rg5329\":\"N\"\n   },\n   \"comprobante\":{\n      \"fecha\":\"20/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"tipo\":\"FACTURA E\",\n      \"operacion\":\"V\",\n      \"punto_venta\":\"0002\",\n      \"numero\":\"00000012\",\n      \"periodo_facturado_desde\":\"28/02/2018\",\n      \"periodo_facturado_hasta\":\"28/02/2018\",\n      \"rubro\":\"Alimentos\",\n      \"rubro_grupo_contable\":\"Alimentos\",\n      \"detalle\":[\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"EXENTO - AVENA INSTANTANEA x5 kg. al 21\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"16098\",\n               \"precio_unitario_sin_iva\":\"100\",\n               \"alicuota\":\"-1\",\n               \"rg5329\":\"N\"\n            },\n            \"leyenda\":\"\"\n         },\n         {\n            \"cantidad\":\"1\",\n            \"producto\":{\n               \"descripcion\":\"p2\",\n               \"unidad_bulto\":\"1\",\n               \"lista_precios\":\"Lista de precios API 3\",\n               \"codigo\":\"160398\",\n               \"precio_unitario_sin_iva\":\"10\",\n               \"alicuota\":\"21\",\n               \"rg5329\":\"N\"\n            },\n            \"leyenda\":\"\"\n         }\n      ],\n      \"bonificacion\":\"0.00\",\n      \"leyenda_gral\":\" \",\n      \"tributos\":[\n         {\n            \"tipo\":6,\n            \"regimen\":2,\n            \"base_imponible\":100,\n            \"alicuota\":10,\n            \"total\":10\n         },\n         {\n            \"tipo\":7,\n            \"regimen\":5,\n            \"base_imponible\":200,\n            \"alicuota\":10,\n            \"total\":20\n         }\n      ],\n      \"impuestos_internos\":\"0\",\n      \"impuestos_internos_base\":\"0\",\n      \"impuestos_internos_alicuota\":\"0\",\n      \"total\":\"142.1\",\n\t\t \"fex\": {\n              \"permisos_tiene\"      : \"S\" ,\n              \"fecha_pago\"          : \"12/10/2019\",\n              \"tipo_exportacion\"    : \"2\",\n              \"pais_comprobante_id\" : \"123\",\n              \"forma_pago_leyenda\"  : \"Payment via paypal 30 days \",\n              \"cliente_pais_cuit\"   : \"50000000016\",\n              \"incoterms_tipo_id\"   : \"FOB\",\n              \"incoterms_nro\"       : \"AAAAGGGGGGGGGGGAAA \",\n              \"permisos\"    : [\n                                  {\n                                      \"codigo_despacho\"  :  \"1234567890123456\",\n                                       \"pais_destino_id\" :    \"112\"\n                                  },\n\n                                  {\n                                      \"codigo_despacho\"   :  \"1234567890144456\",\n                                       \"pais_destino_id\"  :    \"123\"\n                                  },\n                                   {\n                                      \"codigo_despacho\"   :    \"4444567890123456\",\n                                       \"pais_destino_id\"  :    \"145\"\n                                  }\n                              ]\n               \n      }\n\t\t \n   }\n}"

response = http.request(request)
puts response.read_body
```
{% endtab %}
{% endtabs %}



### Información de cada uno de los campos :

| `tipo_exportacion`       | <p>Campo numérico. Longitud 1 caracter. Valores esperados:<br>1= Exportación definitiva de bienes<br>2= Servicios<br>4= Otros.<br><strong>Ejemplo: 2</strong></p>                                                                                                                                                                 |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `permisos_tiene`         | <p>Campo alfabético. Longitud 1 caracter. Indica si se posee documento aduanero de exportación (permiso de embarque). Valores esperados:<br>S= Si posee<br>N= No posee<br>(vacio)= No especifica<br><strong>Ejemplo: S</strong></p>                                                                                               |
| `permisos`               | Solo deberán ser enviados los permisos cuando el campo permisos\_tiene sea igual a "S". Valores a enviar según estructura de datos definida a continuación en ["Permisos de exportacion".](api-factura-electronica-afip-factura-electronica-afip-exportacion.md#estructura-de-permisos)                                            |
| `pais_comprobante_id`    | <p>Campo numérico. Según tabla de referencia <a href="../parametros/consulta-de-paises-afip.md">Paises AFIP (**)</a><br><strong>Ejemplo: 123</strong></p>                                                                                                                                                                          |
| `forma_pago_leyenda`     | <p>Campo alfanumérico. Descripción adicional de la forma de pago<br><strong>Ejemplo: Favor depositar en cuenta XXXXX</strong></p>                                                                                                                                                                                                 |
| `cliente_pais_cuit`      | <p>Campo numérico. Según tabla de referencia <a href="../parametros/consulta-de-cuit-pais-afip.md">CUIT Pais AFIP (**)</a><br><strong>Ejemplo: 51600004380</strong></p>                                                                                                                                                            |
| `incoterms_tipo_id`      | <p>Campo alfabético Incoterms – Cláusula de Venta. Según tabla de referencia <a href="../parametros/consulta-de-incoterms.md">Incoterms (**)</a><br><strong>Ejemplo: EXW</strong></p>                                                                                                                                             |
| `incoterms_nro`          | <p>Campo alfanumérico - Información complementaria del incoterm<br><strong>Ejemplo: Texto dic.</strong></p>                                                                                                                                                                                                                       |
| `comprobantes_asociados` | OPCIONAL. Se deberá informar el/los comprobante/s asociados solamente si el comprobante que se está autorizando corresponde a una Nota de Débito o Nota de Crédito. Según estructura de "[Comprobantes asociados"](api-factura-electronica-afip-factura-electronica-afip-exportacion.md#estructura-de-comprobantes-asociados). |
| fecha\_pago              | Campo fecha - formato esperado: dd/mm/aaaa. Éste campo es obligatorio únicamente para Facturas E, si se envia tipo\_exportacion = 2 o tipo\_exportacion=4                                                                                                                                                                          |

### Estructura de "Permisos "

El bloque de "permisos" es un array con cada uno de los permisos de exportación que dispongas. Cada uno de éstos debe ser enviado acordes a la estructura que se detalla a continuación

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
