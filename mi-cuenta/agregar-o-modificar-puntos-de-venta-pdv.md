---
description: >-
  Integra la API para AFIP de TusFacturasAPP a tu sistema y accede a información
  relacionada con tu cuenta, como agregar o  modificar un punto de venta.
---

# Agregar o modificar puntos de venta (PDV)

### &#x20;Datos a tener en cuenta:

{% hint style="info" %}
**Si estás modificando puntos de venta (PDV)**

* En el caso de la modificación del punto de venta, deberás realizar la solicitud con las keys del punto de venta que querés modificar.
* Ten en cuenta que aquellos puntos de venta que ya posean comprobantes, no podrán modificar su número de CUIT, condición impositiva ni de punto de venta.

**Si estás dando de alta puntos de venta (PDV)**

* Si das de alta un punto de venta de un CUIT que ya existía en TusfacturasAPP y emitía factura electrónica, automáticamente, éste quedará habilitado para emitir factura electrónica AFIP, sin requerir cargar en AFIP un nuevo certificado de seguridad. Lo único que deberás hacer en AFIP, es dar de alta el nuevo punto de venta de tipo "webservices".


{% endhint %}

## Administrar CUIT + Punto de venta

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`puntos_venta/administrar`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción

#### Request Body

| Name                  | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| operacion             | string | <p>Valores esperados: A o M</p><p>A = Alta de nuevo punto de venta</p><p></p><p>M = Modifica el punto de venta, correspondiente a las apikey desde las cuales estoy enviando para hacer el request.</p>                                                                                                                                                                                                                  |
| conceptos\_tipo       | string | <p>Debe indicar el tipo de conceptos que factura, los cuales pueden ser:</p><p>P = Productos</p><p>PS = Productos y Servicios</p><p>S = Servicios</p>                                                                                                                                                                                                                                                                    |
| es\_predeterminado    | string | Indica si el CUIT + Punto de venta es el predeterminado. Valores esperados: S o N                                                                                                                                                                                                                                                                                                                                        |
| esta\_activo          | string | Indica si el CUIT + Punto de venta se encuentra activo y disponible para generar comprobantes. Valores esperados: S o N                                                                                                                                                                                                                                                                                                  |
| mercadopago           | object | Según objeto "mercadopago" que se detalla abajo.                                                                                                                                                                                                                                                                                                                                                                         |
| xero                  | object | Según objeto "xero" que se detalla abajo.                                                                                                                                                                                                                                                                                                                                                                                |
| es\_agente\_retencion | string | Indica si el punto de venta es agente de retención. Valores esperados: S o N.                                                                                                                                                                                                                                                                                                                                            |
| factura               | object | Un objeto del tipo "factura" según se detalla abajo.                                                                                                                                                                                                                                                                                                                                                                     |
| punto\_venta          | number | <p>El número del punto de venta a crear.</p><p>\</p><p>Ej: 4</p>                                                                                                                                                                                                                                                                                                                                                         |
| factura\_afip         | string | <p>Indica si va a querer <a href="https://www.tusfacturas.app/como-empezamos-a-hacer-facturas-electronicas.html">emitir factura electrónica AFIP</a>. En el caso que la respuesta sea "S", se enviará ademas, via email (a la casilla del administrador), el instructivo para realizar el enlace con AFIP, junto con el certificado de seguridad requerido por AFIP.</p><p>\</p><p>Valores esperados: S o N.</p><p>\</p> |
| fecha\_inicio         | string | Fecha de inicio de actividades. Formato: dd/mm/aaaa                                                                                                                                                                                                                                                                                                                                                                      |
| iibb                  | string | El nro de ingresos brutos.                                                                                                                                                                                                                                                                                                                                                                                               |
| iva\_emails           | string | Las direcciones de email separadas por coma donde quieren recibir mensualmente el iva compras-ventas.                                                                                                                                                                                                                                                                                                                    |
| iva\_condicion        | string | La condición impositiva según tabla de referencia.                                                                                                                                                                                                                                                                                                                                                                       |
| direccion             | string | El domicilio fiscal. Dirección + número                                                                                                                                                                                                                                                                                                                                                                                  |
| cuit                  | number | Tu CUIT. Solo números.                                                                                                                                                                                                                                                                                                                                                                                                   |
| razon\_social         | string | La razón social                                                                                                                                                                                                                                                                                                                                                                                                          |
| apitoken              | string | Tus credenciales actuales de acceso.                                                                                                                                                                                                                                                                                                                                                                                     |
| apikey                | string | Tus credenciales actuales de acceso.                                                                                                                                                                                                                                                                                                                                                                                     |
| usertoken             | string | Tus credenciales actuales de acceso.                                                                                                                                                                                                                                                                                                                                                                                     |
| webhook               | string | <p>Campo alfanumérico de hasta 255 caracteres. Formato esperado: https://www.dominio.com/script-nombre.</p><p><a href="../webhooks-notificaciones.md#direccion-del-webhook">Más información</a></p>                                                                                                                                                                                                                      |

#### Objeto "mercadopago"

| Campo a enviar | Descripción                                |
| -------------- | ------------------------------------------ |
| api\_key       | La API KEY obtenida desde MercadoPago.     |
| api\_secret    | La API SECRET obtenieda desde MercadoPago. |

#### Objeto "xero"

| Campo a enviar  | Descripción                                                                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| habilitado      | Indica si se encuentra habilitado o no. Valores esperados: S o N                                                                            |
| consumer\_key   | La consumer KEY obtenida desde XERO                                                                                                         |
| shared\_secret  | La shared\_secret obtenida desde XERO                                                                                                       |
| habilitado\_web | Indica si se encuentra habilitado para sincronizar con XERO cuando se emiten comprobantes desde la plataforma web. Valores esperados: S o N |
| habilitado\_api | Indica si se encuentra habilitado para sincronizar con XERO cuando se emiten comprobantes desde la API. Valores esperados: S o N            |

#### Objeto "factura"

| Campo a enviar                   | Descripcion                                                                                                                                                    |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| leyenda\_general\_predeterminada | Una leyenda predeterminada que saldrá impresa en todos los comprobantes que emitas.                                                                            |
| titulo                           | El titulo que saldrá como encabezado de la factura. En gral se usa la razón social o el nombre de fantasía de la empresa. Máx de caracteres permitidos: 18     |
| subtitulo                        | El subtitulo que saldrá en el encabezado de la factura, bajo el titulo principal. Máx de caracteres permitidos: 18                                             |
| reply\_to\_email                 | La dirección de email para los reply-to en cada envío de comprobante.                                                                                          |
| reply\_to                        | El nombre de quien envía los comprobantes.                                                                                                                     |
| mensaje                          | El mensaje predeterminado que saldrá en el envío de cada comprobante.                                                                                          |
| copias                           | La cantidad de copias que se generan dentro del PDF. Valores esperados: 2= para recibir original y duplicado, 3= para recibir original, duplicado y triplicado |
| cbu                              | Opcional: El número del CBU. Campo numérico, maximo 30 dígitos.                                                                                                |

### JSON De ejemplo a enviar

{% code title="JSON" %}
```
{
   "usertoken":"xxxx",
    "apitoken":"xxx",
    "apikey":"xxxx",
    "operacion":"A",
    "punto_venta": "00023",
    "direccion":"AV. 68 N75A - 50, PISO 4, Buenos Aires, Argentina",
    "razon_social": "MI CUIT DE PRUEBA",
    "cuit": "11111123213",
    "iva_condicion": "M",
    "iva_emails": "tuemail@tudominio.com",
    "iibb":"12345",
    "fecha_inicio": "12/12/2017",
    "factura_afip": "S",
    "es_agente_retencion": "N",
    "esta_activo": "S",
    "es_predeterminado": "S",
    "conceptos_tipo": "PS",
    "webhook": "https://www.dominio.com/script-name",
    "factura" : {
        "leyenda_general_predeterminada": "TEST",
        "titulo" : "PIRULO & CO",
        "subtitulo": "La mejor barberia",
        "reply_to_email": "info@tudominio.com.ar",
        "reply_to": "PIRULO",
        "mensaje": "Le enviamos la factura que se encuentra adjunta",
        "copias": "2"
    }

}
```
{% endcode %}

##

