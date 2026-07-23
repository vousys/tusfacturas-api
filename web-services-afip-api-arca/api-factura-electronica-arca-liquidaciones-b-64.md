---
description: >-
  TusFacturasAPP: API para Facturas A de AFIP/ARCA. Confiable desde 2015. Creada
  por devs y respaldada por expertos impositivos. ¡Los desarrolladores la aman!
icon: code
---

# Liquidaciones B

### Endpoints

Liquidaciones B ( Código ARCA: 0064 )  - emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

Factura A emitida en la modalidad "[Asincrónica](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo_encola`</mark>
{% endhint %}



### JSON para generar una Liquidaciones B en AFIP/ARCA

```json
 {
   "apitoken":"xxxx",
   "usertoken":"xxxx",
   "apikey":"xxxx",
   "cliente":{
      "documento_tipo":"DNI",
      "condicion_iva":"CF",
      "condicion_iva_operacion":"CF",
      "domicilio":"Av Sta Fe 23132",
      "condicion_pago":"201",
      "documento_nro":"111132333",
      "razon_social":"Juan Pedro KJL",
      "provincia":"2",
      "email":"email@dominio.com",
      "reclama_deuda": "N",
      "envia_por_mail":"N",
       "rg5329": "N"
   },
   "comprobante":{
      "rubro":"Sevicios web",
      "tipo":"LIQUIDACIONES B",
      "numero":2134,
      "bonificacion":0,
      "operacion":"V",
      "moneda":"PES",
      "external_reference":"0306-0301",
      "tags": [],
       "datos_informativos": {
	  "paga_misma_moneda": "N"
      },
      "cotizacion": 1,
      "detalle":[
         {
            "cantidad":1,
            "afecta_stock":"S",
            "bonificacion_porcentaje":0,
            "producto":{
               "descripcion":"Hosting pagina web ",
               "codigo":37,
               "lista_precios":"standard",
               "leyenda":"",
               "unidad_bulto":1,
               "alicuota":21,
               "actualiza_precio":"S",
                "unidad_medida": 7,
               "rg5329": "N",
               "precio_unitario_sin_iva":114.88
            }
         }
      ],
      "fecha":"28/03/2018",
      "vencimiento":"26/03/2023",
      "rubro_grupo_contable":"Sevicios",
      "total":139.0, 
      "pagos": {
		"formas_pago": [
		   {"descripcion" : "MercadoPago", "importe" : 139} 			
			   ],
		"total": 139
		},
      "punto_venta":3,
      "tributos":[]
   }
}
```

### ¿Cómo enviar una liquidación B según mi lenguaje de programación?

Podes enviar las facturas A por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado anteriormente.

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

### Parámetros para crear una Liquidación B&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md),  con referencia a cada parámetro y las[ tablas de referencia ](../parametros/tablas-de-referencia.md)necesarias para completar los campos.

#### 📘 Información esencial

Antes de implementar o integrar con nuestra API, asegurate de revisar estos dos recursos fundamentales (¡sí, estos!):

* **Tablas de referencia:** valores, códigos y parámetros que necesitas para que la API funcione correctamente.\
  👉 [Ver tablas de referencia](../parametros/tablas-de-referencia.md)
* **Referencia completa de cada campo de la API:** descripción exacta, tipo de dato y uso correcto de cada parámetro.\
  👉 [Ver referencia de campos](../api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md#estructura-del-json-a-enviar)

### :hand\_splayed: ¿Quién genera una liquidación B?

* **Entidades financieras** comprendidas en la Ley 21.526
* **Compañías de seguros** reguladas por la Ley 20.091
* **Administradoras de tarjetas de crédito y prepagas**, y sistemas de pago por transferencia
* **Instituciones educativas privadas** y entidades de medicina prepaga constituidas como asociaciones o fundaciones
* **Proveedores de Servicios de Activos Virtuales (PSAV)** inscriptos ante la Comisión Nacional de Valores

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

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
