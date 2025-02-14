---
icon: code
description: >-
  TusFacturasAPP: API para Facturas B  sin especificar datos del comprador en
  AFIP/ARCA. Confiable desde 2015. Creada por devs y respaldada por expertos
  impositivos. ¡Los desarrolladores la aman!
---

# Factura B sin especificar datos del comprador

### Endpoints

Factura B emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

Factura B emitida en la modalidad "[Asincrónica](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo_encola`</mark>
{% endhint %}



### JSON para generar una Factura B sin especificar datos del comprador en AFIP/ARCA

```json
{
   "apitoken":"xxxx",
   "usertoken":"xxxx",
   "apikey":"xxxx",
   "cliente":{
      "documento_tipo":"OTRO",
      "condicion_iva":"CF",
       "condicion_iva_operacion":"CF",
      "domicilio":"No especifica",
      "condicion_pago":"201",
      "documento_nro":"0",
      "razon_social":"Consumidor final",
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
```

### ¿Cómo enviar una factura B según mi lenguaje de programación?

Podes enviar las facturas B por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado anteriormente.

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

### PDF de ejemplo de una Factura B

¿Necesitas una factura de ejemplo? [Descárgala ahora.](https://www.tusfacturas.app/app/archivos-modelo/tipos-comprobante/27285051466__FACTURA_B-00010-00000167.pdf) Podes personalizar el diseño accediendo a nuestra [plataforma web](https://www.tusfacturas.app/app/login.html) >  Menú > Mi espacio de trabajo > CUITs/pDV > Editar.

### ¿Quién genera una factura B?

Conocé [desde aqui](../api-factura-electronica-afip-facturacion-ventas/que-tipos-de-comprobante-debo-puedo-emitir.md), quien está obligado a emitir una factura B.

### Datos a tener en cuenta:

{% hint style="info" %}
* En los comprobantes B el IVA se suma al total del producto, pero no aparecerá desglozado en la factura, ya que tu cliente no lo puede discriminar. Vos debes enviar los productos con el precio SIN IVA y su respectiva alícuota de IVA.
* Si queres enviar un comprobante a un consumidor final sin especificar su nombre y DNI,  consulta la siguiente documentación de "[Facturas a Consumidor final sin especificar datos](../api-factura-electronica-afip-facturacion-ventas/facturas-a-consumidor-final-sin-especificar-datos.md)"
{% endhint %}

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
