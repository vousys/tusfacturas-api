---
description: >-
  Servicio API de TusFacturasAPP para emitir notas de crédito C de AFIP/ARCA.
  Confiable desde 2015. ¡Los desarrolladores la aman!
---

# Nota de crédito E

### Endpoints

Nota de crédito E emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

### JSON para generar una Nota de crédito E en AFIP/ARCA con detalle de comprobantes anulados

```json
{
"usertoken" :  "XXXX",
"apikey"    :  "XXXX",
"apitoken"  :  "XXXXXX",
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
                                                    "tipo_comprobante"   :    "FACTURA E",
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

### ¿Cómo enviar una nota de crédito E según mi lenguaje de programación?

Podes enviar las notas de crédito E por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado arriba.

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

### Parámetros para crear una Nota de crédito E&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/),  con referencia a cada parámetro.

### ¿Qué es una nota de crédito E?

Conocé  que es una[ nota de crédito E](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-notas-credito-debito.md).

### ¿Cuándo generar una nota de crédito E?

Conocé [desde aqui](../api-factura-electronica-afip-facturacion-ventas/que-tipos-de-comprobante-debo-puedo-emitir.md), quien está obligado a emitir una nota de crédito E.

### Datos importantes:

{% hint style="info" %}
Solo deberán ser enviados los comprobantes asociados, cuando el campo exportacion\_tipo sea igual a "1" .
{% endhint %}



***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
