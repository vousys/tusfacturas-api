---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para emitir
  comprobantes de venta desde tu sistema actual y obtener la respuesta al
  instante.
---

# Facturación instantánea e individual

TusFacturasAPP es un proveedor líder de servicios de facturación electrónica en Argentina, que permite a empresas de todos los tamaños emitir comprobantes fiscales válidos de manera rápida, segura y cumpliendo con todas las regulaciones de la AFIP.

Integra fácilmente la facturación electrónica en tu software con la API de TusFacturasAPP. Emite comprobantes fiscales válidos desde tu sistema y obtén respuestas inmediatas de la AFIP.

Una vez configurada tu cuenta y creados tus CUIT/Puntos de Venta, podrás comenzar a facturar electrónicamente sin demoras. Revisa nuestras guías "[Cómo empiezo](../como-empiezo.md)" y  "[API Facturación AFIP](./)" para conocer a fondo el servicio y los requerimientos de cada solicitud.

Comienza ya a cumplir con las regulaciones fiscales y brinda una experiencia de facturación digital eficiente a tus clientes. Solicita acceso a nuestra API de facturación electrónica.

## **¿Qué es la facturación instantánea individual?**

Con nuestro servicio API de facturación electrónica instantánea, podrás emitir comprobantes fiscales válidos de manera individual y obtener respuestas en tiempo real desde la AFIP. Al enviar una solicitud a través de nuestra API, el comprobante se procesará de inmediato en nuestra plataforma y recibirás la respuesta al instante. Tené en cuenta que el procesamiento del comprobane en AFIP está sujeta al estado de los servicios AFIP.

Esta opción de facturación electrónica individual te brinda agilidad y eficiencia, permitiéndote integrar fácilmente la emisión de facturas, notas de crédito y otros comprobantes en tu flujo de trabajo actual, cumpliendo con todas las regulaciones fiscales vigentes.

{% hint style="danger" %}
Es crucial monitorear y manejar adecuadamente los errores, ya que los sistemas de la AFIP suelen presentar frecuentes interrupciones o caídas de servicio. Dependiendo del estado de los servicios de la AFIP, la generación de un comprobante fiscal a través de nuestra plataforma puede demorar hasta 1 minuto y 30 segundos. 😰.&#x20;

Nuestro sistema de facturación electrónica cuenta con mecanismos robustos de manejo de errores que te notificarán oportunamente cualquier inconveniente con los servidores de la AFIP. De esta manera, podrás tomar las medidas necesarias y evitar demoras o interrupciones en tus procesos de facturación.

Te sugerimos utilizar el método de [facturación asincrónico](api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md) para evitar éstos inconvenientes.
{% endhint %}

### ¿Cómo crear una venta **instantánea?**

Consulta nuestra guía detallada "[API Facturación AFIP](./)" para conocer a profundidad el servicio, los requerimientos de cada solicitud y los datos específicos que debes enviar para generar nuevos comprobantes de venta. Nuestra documentación completa y ejemplos de código te facilitarán una integración rápida y eficiente de la facturación electrónica en tu sistema actual.

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/nuevo`

Charset: UTF-8

Tipo de dato esperado: JSON&#x20;

#### Request Body

| Name        | Type   | Description                                                                            |
| ----------- | ------ | -------------------------------------------------------------------------------------- |
| usertoken   | string | Tus credenciales de acceso                                                             |
| apitoken    | string | Tus credenciales de acceso                                                             |
| apikey      | string | Tus credenciales de acceso                                                             |
| comprobante | object | Estructura de "comprobante" según se informa en el apartado de ["API facturacion"](./) |
| cliente     | object | Estructura de "Cliente", según se informa en el apartado de ["facturacion"](./)        |

{% tabs %}
{% tab title="200 " %}
{% code title="JSON" %}
```javascript
{
    "error":     "N",
     "errores": [ ""],    
     "rta":      "El comprobante NOTA DE DEBITO B 0002-00000006 (MI CUIT) se ha guardado correctamente",    
     "cae":      "65301278726386 ",
     "requiere_fec":   "NO ",    
     "vencimiento_cae":"07\/08\/2015",    
     "vencimiento_pago":"27\/08\/2015",    
     "comprobante_pdf_url": "https://www.dominio.com/url",
     "afip_qr" : "https://www.afip.gob.ar/fe/qr/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjAyMC0xMS0xNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjAwMDAzIiwidGlwb0NtcCI6MTEsIm5yb0NtcCI6IjAwMDAwMjQ5IiwiaW1wb3J0ZSI6IjAwMDAwMDAwMDAwMDEwMCIsIm1vbmVkYSI6IlBFUyIsImN0eiI6IjAwMDAwMDAwMDAwMDEwMDAwMDAiLCJ0aXBvRG9jUmVjIjo5OSwibnJvRG9jUmVjIjoiMCIsInRpcG9Db2RBdXQiOiJFIiwiY29kQXV0IjoiNzA0NjY4OTk1OTcwOTEifQ== "
     "afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
     "envio_x_mail": "S",
     "external_reference":"ABC123",
     "comprobante_nro": "0000123",
     "comprobante_tipo": "NOTA DE DEBITO B",
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
  
  
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Que te retorna la llamada a la API?

#### &#x20;:white\_check\_mark: Cuando el request resultó exitoso:

Sea cual sea la modalidad que utilices para facturar, por cada comprobante que emitas, obtendrás la siguiente respuesta, con todos los datos que necesitas para almacenar en tu sistema.&#x20;

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

{% hint style="info" %}
Es importante  que descargues toda la información, junto con el pdf y lo almacenes en tu plataforma, ya que si tu cuenta o suscripción no se encuentran vigentes, no podrás obtenerlo.
{% endhint %}

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



