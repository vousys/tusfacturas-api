---
description: El paso a paso para comenzar a integrar TusFacturasAPP, con tu plataforma.
---

# ¿Cómo empiezo?

## Aprende cómo integrar tu software con la API de facturación electrónica AFIP

Crea una cuenta en nuestra plataforma y activa tu plan API DEV para emitir hasta 1.500 comprobantes electrónicos no válidos legalmente durante 1 mes, completamente gratis (exclusivo para nuevas cuentas y por única vez).

### **Explora las funcionalidades de la API y comproba su eficacia en tu proceso de facturación.**

Una vez finalizado el período de prueba, podrás seleccionar el plan API que mejor se adapte a tus necesidades.

**Beneficios del plan API DEV:**

* Emisión gratuita de 1.500 comprobantes electrónicos no válidos legalmente durante 1 mes.
* Ideal para probar la integración y familiarizarte con la API.
* Sin compromisos ni cargos adicionales.

**Comenza tu prueba gratuita hoy mismo y simplifica tu facturación electrónica con la API para AFIP.**

[<mark style="color:purple;">**Crear mi cuenta ahora**</mark>](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html)&#x20;

### Mientras estes en desarrollo:

Para garantizar el cumplimiento legal, nuestra plataforma no dispone de un entorno de pruebas convencional. Esto significa que no podrás enlazar tu CUIT real con AFIP durante las pruebas. Esto evita inconvenientes con el fisco, ya que los comprobantes emitidos en AFIP son inmodificables e irrevocables.

Sin embargo, durante las pruebas, la respuesta que recibirás de nuestra API simulará el comportamiento en producción, los campos CAE y vencimiento del CAE se retornarán vacíos y no se aplicarán las validaciones adicionales de AFIP.

**Para realizar las pruebas, te sugerimos:**

1. Configurar tu CUIT personal con un punto de venta (PDV) irreal (Ej: 679).
2. Una vez finalizadas las pruebas y cuando estés listo para ir a producción, elimina desde nuestra plataforma web todos los comprobantes asociados a ese CUIT/PDV.
3. Da de baja el CUIT/PDV ficticio y crea uno nuevo para enlazarlo con AFIP en producción.

**Recorda:**

* Las pruebas no afectan tu información fiscal real.
* Los comprobantes emitidos durante las pruebas son ficticios y no se registran en AFIP.
* La respuesta de la API durante las pruebas simula el comportamiento en producción.

**¡Comenza a probar la integración con la API para AFIP hoy mismo y prepárate para una facturación electrónica sin complicaciones!**

[<mark style="color:purple;">**Crear mi cuenta ahora**</mark>](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html)&#x20;

{% hint style="info" %}
Te sugerimos revisar nuestros [términos y condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html) para estar al tanto de lo que podes realizar en nuestra plataforma y leer las [FAQs](faqs-or-preguntas-frecuentes.md) para despejar tus dudas.

En caso que necesites asistencia, podes [contactarnos](https://www.tusfacturas.app/contacto.html).
{% endhint %}

### ¿Es realmente fácil crear una venta con TusFacturasAPP?

Si!, crear una venta con TusFacturasAPP es tan fácil como enviar el siguiente JSON para generar una factura B, a la URL:  `https://www.tusfacturas.app/app/api/v2/facturacion/nuevo`&#x20;

```json
{
   "apitoken":"xxxx",
   "apikey":"xxxx",
   "usertoken":"xxxx",
   
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
      "operacion":"V",
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
```

Podes enviarlo por CURL, o por tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos.

{% tabs %}
{% tab title="CURL" %}
```
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
request["User-Agent"] = 'insomnia/9.3.2'
request.body = "{\n   \"apitoken\":\"xxxx\",\n   \"cliente\":{\n      \"documento_tipo\":\"DNI\",\n      \"condicion_iva\":\"CF\",\n      \"domicilio\":\"Av Sta Fe 23132\",\n      \"condicion_pago\":\"201\",\n      \"documento_nro\":\"111132333\",\n      \"razon_social\":\"Juan Pedro KJL\",\n      \"provincia\":\"2\",\n      \"email\":\"email@dominio.com\",\n      \"envia_por_mail\":\"N\",\n       \"rg5329\": \"N\"\n   },\n   \"apikey\":\"xxxx\",\n   \"comprobante\":{\n      \"rubro\":\"Sevicios web\",\n      \"percepciones_iva\":0,\n      \"tipo\":\"FACTURA B\",\n      \"numero\":2134,\n      \"bonificacion\":0,\n      \"operacion\":\"V\",\n      \"detalle\":[\n         {\n            \"cantidad\":1,\n            \"afecta_stock\":\"S\",\n            \"actualiza_precio\":\"S\",\n            \"bonificacion_porcentaje\":0,\n            \"producto\":{\n               \"descripcion\":\"Hosting pagina web \",\n               \"codigo\":37,\n               \"lista_precios\":\"standard\",\n               \"leyenda\":\"\",\n               \"unidad_bulto\":1,\n               \"alicuota\":21,\n               \"actualiza_precio\":\"S\",\n               \"rg5329\": \"N\",\n               \"precio_unitario_sin_iva\":114.88\n            }\n         }\n      ],\n      \"fecha\":\"28/03/2018\",\n      \"vencimiento\":\"26/03/2023\",\n      \"rubro_grupo_contable\":\"Sevicios\",\n      \"total\":139.0,\n      \"cotizacion\":1,\n      \"moneda\":\"PES\",\n      \"punto_venta\":3,\n      \"tributos\":[]\n   },\n   \"usertoken\":\"xxxx\"\n}"

response = http.request(request)
puts response.read_body
```
{% endtab %}
{% endtabs %}

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a hola@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).



¿Qué esperas para comenzar a [emitir factura electrónica AFIP](https://www.tusfacturas.app/como-empezamos-a-hacer-facturas-electronicas.html) con nuestra API?
