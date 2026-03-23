---
description: >-
  Servicio API de TusFacturasAPP para emitir Facturas A bajo la RG5239 de
  AFIP/ARCA. Confiable desde 2015. ¡Los desarrolladores la aman!
icon: code
---

# Factura A - RG5329

### Endpoints

Factura A emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

Factura A emitida en la modalidad "[Asincrónica](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;background-color:purple;">`nuevo_encola`</mark>
{% endhint %}



### JSON para generar una Factura A que percibe IVA por la RG5329 en AFIP/ARCA

```json

{
   "usertoken":"xxxx",
   "apikey":"xxx",
   "apitoken":"xxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"N",
      "condicion_pago":"211",
      "reclama_deuda": "N",
      "condicion_iva":"RI",
       "condicion_iva_operacion":"RI",
      "rg5329":"S"
   },
   "comprobante":{
      "fecha":"26/03/2023",
      "vencimiento":"26/03/2023",
      "tipo":"FACTURA A",
      "operacion":"V",
      "punto_venta":"0002",
      "numero":"00000012",
      "periodo_facturado_desde":"28/02/2018",
      "periodo_facturado_hasta":"28/02/2018",
      "rubro":"Alimentos",
      "rubro_grupo_contable":"Alimentos",
      "detalle":[
         {
            "cantidad":"2",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"Papel carta",
               "unidad_bulto":"1",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":102000,
               "alicuota":21,
               "impuestos_internos_alicuota":0,
               "rg5329":"S",
               "unidad_medida":"7",
               "actualiza_precio":"S"
            },
            "afecta_stock": "S",
            "bonificacion_porcentaje": 0,
            "leyenda":""
         },
         {
            "cantidad":"1",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"Paneles solares",
               "unidad_bulto":"1",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":1000,
               "alicuota":21,
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"N"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"Celulares",
               "unidad_bulto":"1",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":200300,
               "alicuota":10.5,
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"S",
               "rg5329":"S"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         {
            "tipo":6,
            "regimen":3,
            "base_imponible":204000,
            "alicuota":3,
            "total":6120
         },
         {
            "tipo":6,
            "regimen":3,
            "base_imponible":200300,
            "alicuota":1.5,
            "total":3004.5
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
      "total":478526,
      "pagos": {
		      "formas_pago": [
		         {"descripcion" : "MercadoPago", "importe" : 478526} 			
	         ],
		      "total": 478526
		},
      "comprobantes_asociados":[]
   }
}

```

### ¿Cómo enviar una factura A según mi lenguaje de programación?

Podes enviar las notas de crédito A por CURL, o usando tu lenguaje de programación favorito. A continuación te mostramos algunos ejemplos. Reemplaza "TUSFACTURAS\_JSON\_DATA" por el JSON especificado anteriormente.

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

### Parámetros para crear una Factura A&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación avalado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/),  con referencia a cada parámetro.

#### 📘 Información esencial

Antes de implementar o integrar con nuestra API, asegurate de revisar estos dos recursos fundamentales (¡sí, estos!):

* **Tablas de referencia:** valores, códigos y parámetros que necesitas para que la API funcione correctamente.\
  👉 [Ver tablas de referencia](../parametros/tablas-de-referencia.md)
* **Referencia completa de cada campo de la API:** descripción exacta, tipo de dato y uso correcto de cada parámetro.\
  👉 [Ver referencia de campos](../api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md#estructura-del-json-a-enviar)



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



### PDF de ejemplo de una Factura A

¿Necesitas una factura de ejemplo? [Descárgala ahora](https://www.tusfacturas.app/app/archivos-modelo/tipos-comprobante/27285051466__FACTURA_A-00010-00000122.pdf). Podes personalizar el diseño accediendo a nuestra [plataforma web](https://www.tusfacturas.app/app/login.html) >  Menú > Mi espacio de trabajo > CUITs/pDV > Editar.

### ¿Quién genera una factura A RG5329?

Conocé [desde aqui](../api-factura-electronica-afip-facturacion-ventas/que-tipos-de-comprobante-debo-puedo-emitir.md), quien está obligado a emitir una factura A y cuándo aplicar la RG5329, desde nuestras [FAQs](../faqs-or-preguntas-frecuentes.md)

#### Datos a tener en cuenta:

{% hint style="info" %}
A partir del 01-07-2021, todo comprobante A que se emita a un monotributista deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618"._ **Éste dato&#x20;**<mark style="background-color:yellow;">**no debe ser enviado**</mark>**&#x20;en el campo "leyenda\_gral", ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma.**


{% endhint %}

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
