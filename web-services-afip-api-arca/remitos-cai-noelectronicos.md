---
description: >-
  TusFacturasAPP: API para emitir remitos e imprimirlos sobre papel pre-impreso
  con CAI. Confiable desde 2015.
icon: code
---

# Remito para papel pre-impreso con CAI

### Endpoint

Remito - solo en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

### JSON para generar un remito en AFIP/ARCA

{% hint style="info" %}
Los remitos generados en TusFacturasAPP no conectan con ARCA, ARBA ni ningún otro organismo provincial o nacional. Para que tengan validez legal deben imprimirse sobre papel pre-impreso con CAI desde un punto de venta que configures para los remitos.&#x20;

El remito por webservice provisto por ARCA solo está disponible para empresas de ciertos rubros específicos (carnico, lácteo, etc).

Conoce [cómo configurar el diseño del PDF de tus remitos](https://ayuda.tusfacturas.app/es/articles/12044811-como-configurar-el-estilo-de-un-remito-preimpreso-en-imprenta)&#x20;
{% endhint %}

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
      "envia_por_mail":"N",
      "condicion_pago":"211",
      "condicion_iva":"RI",
       "condicion_iva_operacion":"RI"
   },
   "comprobante": {
    "tags": [],
    "tipo": "REMITO",
    "operacion": "V",
    "punto_venta": "10",
    "fecha": "07/01/2026",
    "vencimiento": "10/12/2026",
    "idioma": 1,
    "numero": 0,
    "moneda": "PES",
    "cotizacion": 1,
    "periodo_facturado_desde": "",
    "periodo_facturado_hasta": "",
    "rubro": "Deudores Varios",
    "rubro_grupo_contable": "Ventas",
    "detalle": [
      {
        "cantidad": 1,
        "afecta_stock": "N",
        "leyenda": "Cajon de madera",
        "producto": {
          "codigo": "FR",
          "descripcion": "Cajon de frutas",
          "actualiza_precio": "N",
          "unidad_bulto": 1,
          "lista_precios": "Mayorista",
          "precio_unitario_sin_iva": 100,
          "impuestos_internos_alicuota": 0,
          "alicuota": 21,
          "unidad_medida": 7
        },
        "actualiza_precio": "N",
        "bonificacion_porcentaje": 0
      }
    ],
    "abono": "N",
    "abono_frecuencia": 1,
    "abono_hasta": "",
    "abono_actualiza_precios": "N",
    "bonificacion": 0,
    "leyenda_gral": "",
    "comentario": "",
    "exentos": 0,
    "nogravados": 0,
    "tributos": [],
    "impuestos_internos": "",
    "impuestos_internos_base": "0",
    "impuestos_internos_alicuota": "0",
    "total": 121
  }
}
```

### ¿Cómo enviar un remito según mi lenguaje de programación?

Podes enviar un remito para imprimir sobre papel pre-impreso con CAI por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado arriba.

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

### Parámetros para crear un remito

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/),  con referencia a cada parámetro.

### Respuesta esperada

Consulta la respuesta esperada, según el método que uses para enviarla:

{% content-ref url="../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md" %}
[api-factura-electronica-afip-facturacion-nuevo-comprobante.md](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)
{% endcontent-ref %}



***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
