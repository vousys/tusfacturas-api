---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para emitir
  comprobantes de venta desde tu sistema actual y obtener la respuesta al
  instante.
---

# Facturación instantánea e individual

Una vez configurada tu cuenta y creado tu CUIT+PDV, podrás comenzar a emitir facturas electrónicas.&#x20;

Te sugerimos revisar el apartado de [¿Cómo empiezo?](como-empiezo.md) y luego ["Facturación"](api-factura-electronica-afip-facturacion-ventas.md), para conocer como funciona el servicio y la estructura de cada request que envíes.&#x20;

## **Facturación instantánea individual**

Al utilizar éste servicio, podrás enviar a facturar un (1) comprobante, el mismo impactará de inmediato en nuestra plataforma, y obtendrás la respuesta al instante (siempre y cuando los servicios de AFIP se encuentren funcionando).

{% hint style="danger" %}
Es importante que controles los errores, dado que los servicios de AFIP se caen muy seguido y según funcionen sus servicios, la generación de un comprobante puede llegar a demorar hasta 1,30 minutos 😰. Te sugerimos utilizar el método de [facturación asincrónico](api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md) para evitar éstos inconvenientes.
{% endhint %}

A donde debes enviar el request:&#x20;

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/nuevo" method="post" summary="Nuevo comprobante de Venta" %}
{% swagger-description %}
Charset: UTF-8

Tipo de dato esperado: JSON&#x20;
{% endswagger-description %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" type="object" required="false" %}
Estructura de "comprobante" según se informa en el apartado de 

["facturacion"](api-factura-electronica-afip-facturacion-ventas.md)


{% endswagger-parameter %}

{% swagger-parameter in="body" name="cliente" type="object" required="false" %}
Estructura de "Cliente", según se informa en el apartado de 

["facturacion"](api-factura-electronica-afip-facturacion-ventas.md)


{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}
{% endswagger %}

### Que te retorna la llamada a la API?

#### &#x20;:white\_check\_mark: Cuando el request resultó exitoso:

Sea cual sea la modalidad que utilices para facturar, por cada comprobante que emitas, obtendrás la siguiente respuesta, con todos los datos que necesitas para almacenar en tu sistema.&#x20;

{% hint style="info" %}
Es importante  que descargues toda la información, junto con el pdf y lo almacenes en tu plataforma, ya que si tu cuenta o suscripción no se encuentran vigentes, no podrás obtenerlo.
{% endhint %}

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
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
```

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



####

