---
description: >-
  TusFacturasAPP: Solución SaaS líder en facturación electrónica para empresas.
  Integra nuestra API de facturación AFIP y emití comprobantes desde tu
  plataforma.
icon: i
---

# Facturación instantánea e individual

### ⚡ ¿Qué es la API de facturación individual e instantánea?

La **API de facturación electrónica instantánea de TusFacturasAPP** te permite **emitir comprobantes fiscales válidos ante AFIP/ARCA en tiempo real**, de forma individual. Es ideal para integrar fácilmente la facturación electrónica a tu sistema actual, cumpliendo con las normativas fiscales vigentes en Argentina.

### ¿Qué podes hacer con la API para facturación AFIP?

Integra fácilmente la facturación electrónica en tu software con la API de TusFacturasAPP. Emite comprobantes fiscales válidos desde tu sistema y obtén respuestas inmediatas de la AFIP.

<figure><img src="../.gitbook/assets/157.webp" alt="SDK AFIP. TusFacturasAPP API Factura Electronica AFIP. "><figcaption></figcaption></figure>

### ¿Cómo empiezo?

Te sugerimos revisar la guia de [¿Cómo empiezo?](../como-empiezo/) . Una vez configurada tu cuenta y creado tu CUIT/Punto de venta (PDV) en TusFacturasAPP, podrás comenzar a emitir facturas electrónicas AFIP Argentina válidas.&#x20;

### Características de la facturación individual e instantánea

Esta modalidad se caracteriza por brindar una **respuesta inmediata del servicio de AFIP**, permitiéndote generar facturas, notas de crédito, notas de débito y otros tipos de comprobantes sin demoras innecesarias.

> 📌 **Importante:** La respuesta inmediata depende directamente del estado de los servidores de AFIP/ARCA. En momentos de alta carga o interrupciones, el proceso puede tardar hasta **1 minuto y 30 segundos** o más. Nuestro sistema de facturación electrónica cuenta con mecanismos robustos de manejo de errores que te notificarán oportunamente cualquier inconveniente con los servidores de la AFIP. De esta manera, podrás tomar las medidas necesarias y evitar demoras o interrupciones en tus procesos de facturación.
>
> Te sugerimos utilizar siempre que puedas, el método de [facturación asincrónico](api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md) para evitar éstos inconvenientes.

### 🔍 ¿Qué ventajas ofrece este método?

* ✅ Emisión inmediata de comprobantes válidos ante AFIP/ARCA.
* ✅ Integración directa con tus sistemas o plataformas.
* ✅ Ideal para puntos de venta, ecommerce o sistemas que requieren respuesta en tiempo real.
* ✅ Compatible con todos los tipos de comprobantes: facturas, NC, ND, remitos, presupuestos, pedidos, etc.

### ⚠️ Consideraciones clave sobre errores y estabilidad

Los servicios de AFIP pueden presentar **intermitencias frecuentes**. Por eso, **TusFacturasAPP incluye un sistema robusto de manejo de errores**, que te notifica en caso de fallas o demoras del servicio oficial.

* 🔔 Si la respuesta contiene errores, recibirás un campo `"error": "S"` y una lista detallada en `"errores"`, para facilitar el diagnóstico.
* 🧩 Si el comprobante se genera correctamente, recibirás toda la información fiscal junto con los enlaces al archivo PDF.

> 🛑 **Recomendación:** Si tu aplicación requiere máxima estabilidad, considerá usar la modalidad **asincrónica**, que coloca los comprobantes en una cola de procesamiento automática. Esto ayuda a evitar interrupciones causadas por caídas en los servidores de AFIP.

### 🚀 ¿Cómo crear una venta instantánea?

Consultá nuestra [guía completa 👉 **“Referencia API AFIP ARCA”**](referencia-api-afip-arca.md), donde encontrarás:

* Especificaciones técnicas
* Campos requeridos para armar el request
* [Ejemplos de código](../web-services-afip-api-arca/) listos para usar
* Buenas prácticas de integración y manejo de errores

> Con nuestra documentación clara y ejemplos reales, **la integración de la facturación electrónica en tu software será rápida, sencilla y confiable**.

### 📌 Endpoint para ventas individuales e instantáneas:

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`nuevo`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.
{% endhint %}

Charset: UTF-8 / JSON&#x20;

#### Body

| Name        | Type   | Description                                                                                                                             |
| ----------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| usertoken   | string | Tus credenciales de acceso                                                                                                              |
| apitoken    | string | Tus credenciales de acceso                                                                                                              |
| apikey      | string | Tus credenciales de acceso                                                                                                              |
| comprobante | object | Estructura de "comprobante" según se informa en la [referencia API](referencia-api-afip-arca.md#estructura-del-bloque-comprobante)      |
| cliente     | object | Estructura de "Cliente", según se informa en la [referencia API](referencia-api-afip-arca.md#estructura-del-bloque-cliente-y-proveedor) |



### ¿Qué te retorna la llamada a la API de facturación AFIP/ARCA en la modalidad individual e instantánea?

#### &#x20;:white\_check\_mark: Cuando el request resultó exitoso:

Cuando un comprobante se emite correctamente en modalidad individual e instantánea, recibirás:

```
{
    "error":     "N",
     "errores": [ ""],    
     "rta":      "El comprobante NOTA DE DEBITO B 0002-00000006 (MI CUIT) se ha guardado correctamente",    
     "cae":      "65301278726386 ",
     "requiere_fec":   "NO ",    
     "vencimiento_cae":"07\/08\/2015",    
     "vencimiento_pago":"27\/08\/2015",    
     "comprobante_pdf_url": "https://www.dominio.com/url",
     "comprobante_ticket_url": "https://www.dominio.com/url",
     "afip_qr" : "https://www.afip.gob.ar/fe/qr/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjAyMC0xMS0xNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjAwMDAzIiwidGlwb0NtcCI6MTEsIm5yb0NtcCI6IjAwMDAwMjQ5IiwiaW1wb3J0ZSI6IjAwMDAwMDAwMDAwMDEwMCIsIm1vbmVkYSI6IlBFUyIsImN0eiI6IjAwMDAwMDAwMDAwMDEwMDAwMDAiLCJ0aXBvRG9jUmVjIjo5OSwibnJvRG9jUmVjIjoiMCIsInRpcG9Db2RBdXQiOiJFIiwiY29kQXV0IjoiNzA0NjY4OTk1OTcwOTEifQ== "
     "afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
     "envio_x_mail": "S",
     "external_reference":  "ABC123",
     "comprobante_nro": "0000123",
     "comprobante_tipo": "NOTA DE DEBITO B",
        "micrositios": {
			"cliente": "url-del-micrositio",
			"descarga":"url-del-micrositio"
		     },
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
```

📁 **Importante:** La URL de descarga del PDF es temporal, por lo que es esencial que descargues y guardes los archivos generados (PDF en hoja A4/ticket para papel de 80mm), ya que si tu cuenta o suscripción vence, **no podrás volver a acceder a esos documentos** desde la API.&#x20;



#### :octagonal\_sign: Response con error

En caso de detectar error, la variable "error" contendrá una "S" y "errores" una lista con todos los errores encontrados

```
{
  "error": "S",
  "errores": [
   "El tipo de documento enviado no es valido",
    "Para la condicion de IVA seleccionada no se permite realizar comprobantes de tipo B."
  ],
  "external_reference": "ABC123",
  "error_cod": [],
  "error_details": [
    {
      "code": "TFC-8004",
      "text": "Para la condicion de IVA seleccionada no se permite realizar comprobantes de tipo B."
    }
  ]
}
```



### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

***

[TusFacturasAPP](https://www.tusfacturas.app) es un proveedor [SaaS](https://www.tusfacturas.app/saas-facturacion-b2b-argentina.html) líder de servicios de [facturación electrónica en Argentina](https://www.tusfacturas.app/factura-electronica-afip.html), que permite a empresas de todos los tamaños emitir comprobantes fiscales válidos de manera rápida, segura y cumpliendo con todas las regulaciones de la AFIP.
