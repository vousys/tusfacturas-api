---
description: >-
  TusFacturasAPP: API para Notas de crédito MiPyme A de AFIP/ARCA. Confiable
  desde 2015. Creada por devs y respaldada por expertos impositivos. ¡Los
  desarrolladores la aman!
icon: code
---

# Nota de crédito MiPyme A

### Endpoints

Nota de crédito MiPyme A emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

### JSON para generar una Nota de crédito MiPyme A en AFIP/ARCA con detalle de comprobantes anulados

<pre class="language-json"><code class="lang-json"><strong>{
</strong>    "usertoken": "XXX",
    "apikey": XXX,
    "apitoken": "XXXX",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"1111111111",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"26",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI",
       "condicion_iva_operacion":"RI"
   },
   "comprobante":{
      "fecha":"14/01/2025",
      "tipo":"NOTA DE CREDITO ELECTRONICA MiPyME (FCE) A",
      "vencimiento":"26/03/2025",
      "operacion":"V",
      "punto_venta":"0010",
      "moneda":"DOL",
      "idioma":"2",
      "cotizacion":"1115.20",
      "tags": [ 
	"etiqueta1","etiqueta2"
       ],
       "datos_informativos": {
	  "paga_misma_moneda": "N"
      },
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
      "rg_especiales": {
		"regimen": "Factura de Cr\u00e9dito Electr\u00f3nica MiPyMEs (FCE)",
		"datos": [{
				"id": 22,
				"valor": "N"
			},
			{
				"id": 23,
				"valor": "PIRULO S.A"
			},
			{
				"id": 27,
				"valor": "SCA"
			}
		]
	},
        "comprobantes_asociados": [
                            {
                               "tipo_comprobante"   :    "FACTURA DE CREDITO ELECTRONICA MiPyME (FCE) A",
                                "punto_venta"  :    "10",
                                 "numero" : 12313,
                                "cuit": 1111111111, 
                                "comprobante_fecha":"07/07/2025"     
                             } 
                         ] 
        }
}
</code></pre>

### ¿Cómo enviar una nota de crédito MiPyme A según mi lenguaje de programación?

Podes enviar las notas de crédito MiPyme A por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado arriba.

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

### Parámetros para crear una Nota de crédito MiPyme A&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/),  con referencia a cada parámetro.

### ¿Qué es una nota de crédito MiPyme A?

Conocé  que es una [nota de crédito ](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce.md)MiPyme A.

### ¿Cuándo generar una nota de crédito MiPyme A?

Conocé [desde aqui](../api-factura-electronica-afip-facturacion-ventas/que-tipos-de-comprobante-debo-puedo-emitir.md), quien está obligado a emitir una nota de crédito MiPyme A.



***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
