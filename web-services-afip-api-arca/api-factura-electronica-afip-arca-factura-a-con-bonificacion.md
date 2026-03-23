---
description: >-
  Servicio API de TusFacturasAPP para emitir Facturas A con bonificaciones de
  AFIP/ARCA. Confiable desde 2015. ¡Los desarrolladores la aman!
icon: code
---

# Factura A con bonificaciones

### Endpoints

Factura A emitida en la modalidad "[Instantánea](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`nuevo`</mark>
{% endhint %}

Factura A emitida en la modalidad "[Asincrónica](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)"

{% hint style="info" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;background-color:purple;">`nuevo_encola`</mark>
{% endhint %}



### JSON para generar una Factura A con bonificaciones porcentuales a nivel producto

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
      "reclama_deuda": "N",
      "condicion_iva":"RI",
       "condicion_iva_operacion":"RI"
   }, 
    "comprobante": {
        "external_reference": "0306-0301",
        "tags": [],
        "tipo": "FACTURA A",
        "operacion": "V",
        "punto_venta": "10",
        "fecha": "14/11/2024",
        "vencimiento": "26/12/2024",
        "idioma": 1,
        "numero": 0,
        "moneda": "PES",
        "cotizacion": 3,
        "periodo_facturado_desde": "",
        "periodo_facturado_hasta": "",
        "rubro": "Deudores Varios",
        "rubro_grupo_contable": "Ventas",
        "detalle": [
            {
                "cantidad": 1,
                "afecta_stock": "N",
                "leyenda": " Color rojo",
                "producto": {
                    "codigo": "LAPICERA1",
                    "descripcion": "LAPICERAS BIC",
                    "actualiza_precio": "N",
                    "unidad_bulto": 1,
                    "lista_precios": "LAPICERAS",
                    "precio_unitario_sin_iva": 100,
                    "impuestos_internos_alicuota": 0,
                    "alicuota": 21,
                    "unidad_medida": 7
                },
                "actualiza_precio": "S",
                "bonificacion_porcentaje": 20
            }
        ],
        "abono": "N",
        "abono_frecuencia": 1,
        "abono_hasta": "11\/2024",
        "abono_actualiza_precios": "N",
        "bonificacion": 0,
        "leyenda_gral": "",
        "comentario": "", 
        "total": 96.8,
        "pagos": {
            "formas_pago": [
                {
                    "descripcion": "MercadoPago",
                    "importe": 50
                },
                {
                    "descripcion": "Pago con especies",
                    "importe": 20
                }
            ],
            "total": 70
        }
    } 
}
    
```

### JSON para generar una Factura A con bonificaciones monetarias a nivel comprobante



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
      "reclama_deuda": "N",
      "condicion_pago":"211",
      "condicion_iva":"RI"
   }, 
    "comprobante": {
        "external_reference": "0306-0301",
        "tags": [
            "etiqueta1",
            "etiqueta2"
        ],
        "tipo": "FACTURA A",
        "operacion": "V",
        "punto_venta": "10",
        "fecha": "14/11/2024",
        "vencimiento": "26/12/2024",
        "idioma": 1,
        "numero": 0,
        "moneda": "PES",
        "cotizacion": 3,
        "periodo_facturado_desde": "",
        "periodo_facturado_hasta": "",
        "rubro": "Deudores Varios",
        "rubro_grupo_contable": "Ventas",
        "detalle": [
            {
                "cantidad": 1,
                "afecta_stock": "N",
                "leyenda": " Color rojo",
                "producto": {
                    "codigo": "LAPICERA1",
                    "descripcion": "LAPICERAS BIC",
                    "actualiza_precio": "N",
                    "unidad_bulto": 1,
                    "lista_precios": "LAPICERAS",
                    "precio_unitario_sin_iva": 100,
                    "impuestos_internos_alicuota": 0,
                    "alicuota": 21,
                    "unidad_medida": 7
                },
                "actualiza_precio": "S",
                "bonificacion_porcentaje": 0
            }
        ],
        "abono": "N",
        "abono_frecuencia": 1,
        "abono_hasta": "11\/2024",
        "abono_actualiza_precios": "N",
        "bonificacion": 20,
        "leyenda_gral": "",
        "comentario": "",
         
        "total": 96.8,
        "pagos": {
            "formas_pago": [
                {
                    "descripcion": "MercadoPago",
                    "importe": 50
                },
                {
                    "descripcion": "Pago con especies",
                    "importe": 20
                }
            ],
            "total": 70
        }
    } 
}
    json
```

### ¿Cómo enviar una factura A con descuentos según mi lenguaje de programación?

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

### Parámetros para crear una Factura A con bonificaciones&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación avalado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina.&#x20;

Consulta la [documentación de la API de facturación AFIP/ARCA](../api-factura-electronica-afip-facturacion-ventas/),  con referencia a cada parámetro y conoce otras[ alternativas de cómo enviar bonificaciones](../api-factura-electronica-afip-facturacion-ventas/ejemplo-de-factura-con-bonificaciones-descuentos.md).

{% content-ref url="../api-factura-electronica-afip-facturacion-ventas/ejemplo-de-factura-con-bonificaciones-descuentos.md" %}
[ejemplo-de-factura-con-bonificaciones-descuentos.md](../api-factura-electronica-afip-facturacion-ventas/ejemplo-de-factura-con-bonificaciones-descuentos.md)
{% endcontent-ref %}

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

#### Datos a tener en cuenta:

{% hint style="info" %}
A partir del 01-07-2021, todo comprobante A que se emita a un monotributista deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618"._ **Éste dato&#x20;**<mark style="background-color:yellow;">**no debe ser enviado**</mark>**&#x20;en el campo "leyenda\_gral", ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma.**


{% endhint %}

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).&#x20;

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
