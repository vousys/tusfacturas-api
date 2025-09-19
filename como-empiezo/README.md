---
description: >-
  Conoce la guía paso a pase para integrar tu software con la API de facturación
  electrónica AFIP de TusFacturasAPP. Elegida por todos los desarrolladores
  desde 2015.
---

# 🎯 ¿Cómo empiezo?

### ¿Qué es TusFacturasAPP?

TusFacturasAPP es la API líder en Argentina para integrar facturación electrónica AFIP/ARCA en tu software. Elegida por desarrolladores desde 2015, te permite emitir facturas electrónicas de forma simple y confiable.

#### 🏆 ¿Por qué confiar en TusFacturasAPP?

**Respaldo profesional dual:** Contamos con el soporte de un estudio contable especializado que nos mantiene actualizados con las últimas normativas fiscales de Argentina, y [VOUSYS](https://www.vousys.com/), una empresa de desarrollo de software con +20 años de experiencia, que garantiza que tu integración requiera la menor cantidad de cambios posibles.

**Esto significa para tu desarrollo:**

* ✅ **Cumplimiento normativo garantizado** - Siempre al día con AFIP/ARCA
* ✅ **Estabilidad en la integración** - Menos cambios en tu código
* ✅ **Soporte técnico especializado** - Respaldado por profesionales contables y de desarrollo
* ✅ **Actualizaciones transparentes** - Te notificamos cualquier cambio con anticipación

### 🎯 Comenzá en 3 Pasos

{% stepper %}
{% step %}
#### Creá tu Cuenta de Desarrollo

* [**Registrate gratis desde aquí**](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html)&#x20;
* Se activará automáticamente tu **Plan API DEV** por 30 días
* Podrás emitir hasta **1.500 comprobantes de prueba** sin costo
{% endstep %}

{% step %}
#### Configurá tus Credenciales

* Ingresá a **Menú > Mi espacio de trabajo > Puntos de venta**
* Configurá tu CUIT personal con un punto de venta de prueba (ej: 679)
* Una vez creado el punto de venta, tendrás disponible las credenciales API. En caso de no visualizarlas, significa que tu plan actual no corresponde a API DEV. [Contactános](https://tusfacturas.app/contacto.html) y lo resolvemos.
{% endstep %}

{% step %}
#### Realizá tu Primera Integración

[Enviá una petición POST](../web-services-afip-api-arca/) a nuestra API y comenzá a facturar inmediatamente.
{% endstep %}
{% endstepper %}

### 🔧 Entorno de Desarrollo

#### ¿Por qué no hay un entorno de pruebas tradicional?

Para garantizar el cumplimiento legal, no disponemos de un entorno de pruebas convencional. Esto significa que:

* ✅ **No podrás enlazar tu CUIT real** con AFIP/ARCA durante las pruebas
* ✅ **Evitás inconvenientes fiscales** ya que los comprobantes AFIP son inmodificables
* ✅ **La respuesta simula el comportamiento de producción** con campos CAE vacíos
* ✅ **No se aplican validaciones adicionales** de AFIP/ARCA durante las pruebas

### Beneficios del Plan API DEV

| Característica    | Detalle                                                                                                                                        |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duración**      | 30 días completamente gratis                                                                                                                   |
| **Comprobantes**  | Hasta 1.500 facturas de prueba desde 2 puntos venta                                                                                            |
| **Validez legal** | No válidos legalmente (solo para desarrollo)                                                                                                   |
| **Soporte**       | **Ilimitado** desde nuestro centro de ayuda. Contamos con atención personalizada por e-mail o chat, de lunes a viernes de 09 a 15:30hs (GMT-3) |



{% hint style="info" %}
Te sugerimos revisar nuestros [términos y condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html) para estar al tanto de lo que podes realizar en nuestra plataforma y leer las [FAQs](../faqs-or-preguntas-frecuentes.md) para despejar tus dudas.

En caso que necesites asistencia, podes [contactarnos](https://www.tusfacturas.app/contacto.html).
{% endhint %}

### 💻 Tu Primera Factura  en 2 Minutos

#### ¿Es realmente fácil crear una venta con TusFacturasAPP?

¡Si! Crear una venta con TusFacturasAPP es tan fácil como enviar el siguiente JSON para crear una factura B

#### Endpoint de Facturación

```
POST https://www.tusfacturas.app/app/api/v2/facturacion/nuevo
```

&#x20;JSON:

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

Podes enviarlo por CURL, o por tu lenguaje de programación favorito.&#x20;

A continuación te mostramos algunos ejemplos. Para conocer el detalle de cada campo,  accede desde [aquí](../api-factura-electronica-afip-facturacion-ventas/) a la documentación.

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

### Espacios de trabajo y puntos de venta en TusFacturasAPP

Antes de comenzar a programar, tómate un momento para familiarizarte con los siguientes artículos de ayuda, que cubren temas esenciales como el manejo de **Puntos de Venta**, la estructura de los **Espacios de Trabajo** y las consideraciones para la **gestión de múltiples clientes**.

**Artículos de referencia:**

* [Qué es un punto de venta](https://ayuda.tusfacturas.app/es/articles/10421730-que-es-un-punto-de-venta)
* [Qué es un espacio de trabajo](https://app.gitbook.com/u/moL4BIMnO2SlXqOeMjlT1FpUmH63)
* [Manejar múltiples puntos de venta en un mismo espacio de trabajo](https://ayuda.tusfacturas.app/es/articles/10533387-es-posible-manejar-multiples-puntos-de-venta-en-un-mismo-espacio-de-trabajo)
* [Gestión de múltiples clientes: espacios de trabajo separados vs. único](https://ayuda.tusfacturas.app/es/articles/11839614-gestion-de-multiples-clientes-conviene-espacios-de-trabajo-separados-vs-unico)

### Algunos ejemplos de como facturar una venta según su tipo / letra

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-factura-a.md" %}
[api-factura-electronica-afip-factura-a.md](../web-services-afip-api-arca/api-factura-electronica-afip-factura-a.md)
{% endcontent-ref %}

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-factura-b.md" %}
[api-factura-electronica-afip-factura-b.md](../web-services-afip-api-arca/api-factura-electronica-afip-factura-b.md)
{% endcontent-ref %}

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-factura-c.md" %}
[api-factura-electronica-afip-factura-c.md](../web-services-afip-api-arca/api-factura-electronica-afip-factura-c.md)
{% endcontent-ref %}

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-factura-e.md" %}
[api-factura-electronica-afip-factura-e.md](../web-services-afip-api-arca/api-factura-electronica-afip-factura-e.md)
{% endcontent-ref %}

{% content-ref url="../web-services-afip-api-arca/api-factura-electronica-afip-factura-mypyme-a.md" %}
[api-factura-electronica-afip-factura-mypyme-a.md](../web-services-afip-api-arca/api-factura-electronica-afip-factura-mypyme-a.md)
{% endcontent-ref %}

📋 Tipos de Comprobantes Disponibles

La API soporta todos los tipos de comprobantes AFIP:

* **Facturas A, B, C, M**
* **Notas de Crédito y Débito**
* **Recibos**
* **Comprobantes de Exportación**
* **Facturación Electrónica MiPyME (FCE)**

[Ver documentación completa de tipos de comprobantes](../api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md)

***

### 🔄 Después del Período de Prueba

Una vez finalizado tu período de prueba de 30 días, podrás:

1. **Seleccionar el plan que mejor se adapte** a tu volumen de facturación
2. **Migrar a producción** con validaciones AFIP/ARCA completas
3. **Emitir facturas con validez legal** vinculadas a tu CUIT real

[Ver planes y tarifas disponibles](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html)

***

### 🚨 Puntos Importantes a Recordar

* ⚠️ **Las pruebas NO afectan tu información fiscal real** (plan API DEV no se conecta con AFIP/ARCA)
* ⚠️ **Los comprobantes de prueba son ficticios** y no se registran en AFIP/ARCA
* ⚠️ **La respuesta durante las pruebas simula el comportamiento de producción**
* ⚠️ **Los campos CAE y vencimiento CAE se devuelven vacíos** en modo desarrollo

***

### 🆘 ¿Necesitás Ayuda?

#### Soporte Técnico

Si tenés dudas sobre la integración o necesitás asistencia:

* **📧 Email**: api@tusfacturas.app
* **💬 Chat en vivo**: Disponible en [www.tusfacturas.app](https://www.tusfacturas.app)&#x20;



***

### 🏁 ¡Comenzá Ahora!

¿Qué esperás para comenzar a emitir facturas electrónicas ARCA con nuestra API?

[**🚀 Crear cuenta gratuita ahora**](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html)[.](../api-factura-electronica-afip-facturacion-ventas/)

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

[ ](../api-factura-electronica-afip-facturacion-ventas/)



¿Qué esperas para comenzar a [emitir factura electrónica AFIP](https://www.tusfacturas.app/como-empezamos-a-hacer-facturas-electronicas.html) con nuestra API?
