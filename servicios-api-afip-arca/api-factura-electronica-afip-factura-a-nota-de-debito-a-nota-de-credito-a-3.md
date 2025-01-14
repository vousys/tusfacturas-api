---
description: >-
  Servicio API de TusFacturasAPP para emitir Facturas E de AFIP/ARCA. Confiable
  desde 2015. ¡Los desarrolladores la aman!
---

# Factura E

### Endpoints

Factura E emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

### JSON para generar una Factura E en AFIP/ARCA

```json
{
    "usertoken": "XXX",
    "apikey": XXX,
    "apitoken": "XXXX",
   "cliente":{
      "documento_tipo":"OTRO",
      "documento_nro":"11124445",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"26",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"CDEX"
   },
   "comprobante":{
      "fecha":"14/01/2025",
      "tipo":"FACTURA E",
      "vencimiento":"26/03/2025",
      "operacion":"V",
      "punto_venta":"0010",
      
      "periodo_facturado_desde":"01/02/2025",
      "periodo_facturado_hasta":"28/02/2025",
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
               "alicuota":"0",
               "rg5329":"N"
            },
            "leyenda":"Enviadas en cajas separadas"
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":"100",
     "fex": {
              "permisos_tiene"      : "" ,
              "fecha_pago"          : "12/02/2025",
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
}
```

### ¿Cómo enviar una factura E según mi lenguaje de programación?

Podes enviar las facturas E por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado anteriormente.

{% tabs %}
{% tab title="CURL" %}
```sh
curl --request POST \
  --url https://www.tusfacturas.app/app/api/v2/facturacion/nuevo \
  --header 'Content-Type: application/json' \
  --data ' 
     TUSFACTURAS_JSON_DATA
     '
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
  CURLOPT_POSTFIELDS => "TUSFACTURAS_JSON_DATA",
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

payload = "TUSFACTURAS_JSON_DATA"

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
  data: TUSFACTURAS_JSON_DATA
   
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
request.body = "TUSFACTURAS_JSON_DATA"

response = http.request(request)
puts response.read_body
```
{% endtab %}
{% endtabs %}

### Parámetros para armar el JSON&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/),  con referencia a cada parámetro.

### ¿Quién genera una factura E?

Conocé [desde aqui](../que-tipos-de-comprobante-debo-puedo-emitir.md), quien está obligado a emitir una factura E.

### Datos a tener en cuenta:

{% hint style="info" %}
* Los comprobantes E no llevan IVA, tributos, bonificaciones, conceptos no gravados ni impuestos internos.
{% endhint %}

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
