---
description: >-
  TusFacturasAPP: API para Facturas C de AFIP/ARCA. Confiable desde 2015. Creada
  por devs y respaldada por expertos impositivos. ¡Los desarrolladores la aman!
icon: code
---

# Factura C

### Endpoints

Factura C emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

Factura C emitida en la modalidad "[Asincrónica](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo_encola`</mark>
{% endhint %}



### JSON para generar una Factura C en AFIP/ARCA

{% hint style="info" %}
Los comprobantes de tipo "C" deben llevar alícuota de IVA = 0 y no pueden incluir exentos, no gravados ni percepciones
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
      "reclama_deuda": "N",
      "envia_por_mail":"N",
      "condicion_pago":"211",
      "condicion_iva":"RI",
       "condicion_iva_operacion":"RI"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"FACTURA C",
      "external_reference":"0306-0301",
      "tags": [ 
	"etiqueta1","etiqueta2"
       ],
       "datos_informativos": {
			   "paga_misma_moneda": "N"
			},	
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
                "unidad_medida": 7,
                "actualiza_precio":"S",
               "alicuota":"0"
            },
            "afecta_stock": "S",
            "bonificacion_porcentaje": 0,
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
         "pagos": {
		"formas_pago": [
		   {"descripcion" : "MercadoPago", "importe" : 110} 			
			   ],
		"total": 110
		}, 
   }
}
```

### ¿Cómo enviar una factura C según mi lenguaje de programación?

Podes enviar las facturas C por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado anteriormente.

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

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md),  con referencia a cada parámetro.

### Respuesta esperada

Consulta la respuesta esperada, según el método que uses para enviarla:

{% content-ref url="../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md" %}
[api-factura-electronica-afip-facturacion-nuevo-comprobante.md](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)
{% endcontent-ref %}

{% content-ref url="../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md" %}
[api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)
{% endcontent-ref %}

{% content-ref url="../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-api-facturacion-por-lotes.md" %}
[api-factura-electronica-afip-api-facturacion-por-lotes.md](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-api-facturacion-por-lotes.md)
{% endcontent-ref %}



### PDF de ejemplo de una Factura C

¿Necesitas una factura de ejemplo? [Descárgala ahora](https://www.tusfacturas.app/app/archivos-modelo/tipos-comprobante/27285051466__FACTURA_C-00010-00000003.pdf). Podes personalizar el diseño accediendo a nuestra [plataforma web](https://www.tusfacturas.app/app/login.html) >  Menú > Mi espacio de trabajo > CUITs/pDV > Editar.

### ¿Quién genera una factura C?

Conocé [desde aqui](../api-factura-electronica-afip-facturacion-ventas/que-tipos-de-comprobante-debo-puedo-emitir.md), quien está obligado a emitir una factura C.

### Datos a tener en cuenta:

{% hint style="info" %}
* Los comprobantes C no llevan IVA.
* Si queres enviar un comprobante a un consumidor final sin especificar su nombre y DNI,  consulta la siguiente documentación de "[Facturas a Consumidor final sin especificar datos](../api-factura-electronica-afip-facturacion-ventas/facturas-a-consumidor-final-sin-especificar-datos.md)"
{% endhint %}

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
