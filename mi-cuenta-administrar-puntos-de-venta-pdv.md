# Mi cuenta - Administrar puntos de venta (PDV)

Con la API de TusFacturasAPP, podrás administrar tus puntos venta, crearlos, editarlos, solicitar el certificado de enlace con AFIP y hasta predeterminarlos.&#x20;

## Agregar o modificar puntos de venta

### &#x20;Datos a tener en cuenta:

{% hint style="info" %}
**Si estás modificando puntos de venta (PDV)**

* En el caso de la modificación del punto de venta, deberás realizar la solicitud con las keys del punto de venta que querés modificar.
* Ten en cuenta que aquellos puntos de venta que ya posean comprobantes, no podrán modificar su número de CUIT, condición impositiva ni de punto de venta.

**Si estás dando de alta puntos de venta (PDV)**

* Si das de alta un punto de venta de un CUIT que ya existía en TusfacturasAPP y emitía factura electrónica, automáticamente, éste quedará habilitado para emitir factura electrónica AFIP, sin requerir cargar en AFIP un nuevo certificado de seguridad. Lo único que deberás hacer en AFIP, es dar de alta el nuevo punto de venta de tipo "webservices".

****
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/puntos_venta/administrar" method="post" summary="Administrar CUIT + Punto de venta" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="operacion" type="string" required="false" %}
Valores esperados: A o M

A = Alta de nuevo punto de venta



M = Modifica el punto de venta, correspondiente a las apikey desde las cuales estoy enviando para hacer el request.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="conceptos_tipo" type="string" required="false" %}
Debe indicar el tipo de conceptos que factura, los cuales pueden ser:

P = Productos

PS = Productos y Servicios

S = Servicios
{% endswagger-parameter %}

{% swagger-parameter in="body" name="es_predeterminado" type="string" required="false" %}
Indica si el CUIT + Punto de venta es el predeterminado. Valores esperados: S o N
{% endswagger-parameter %}

{% swagger-parameter in="body" name="esta_activo" type="string" required="false" %}
Indica si el CUIT + Punto de venta se encuentra activo y disponible para generar comprobantes. Valores esperados: S o N
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mercadopago" type="object" required="false" %}
Según objeto "mercadopago" que se detalla abajo.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="xero" type="object" required="false" %}
Según objeto "xero" que se detalla abajo.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="es_agente_retencion" type="string" required="false" %}
Indica si el punto de venta es agente de retención. Valores esperados: S o N.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="factura" type="object" required="false" %}
Un objeto del tipo "factura" según se detalla abajo.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="punto_venta" type="number" required="false" %}
El número del punto de venta a crear.

\\

Ej: 4
{% endswagger-parameter %}

{% swagger-parameter in="body" name="factura_afip" type="string" required="false" %}
Indica si va a querer emitir factura electrónica AFIP. En el caso que la respuesta sea "S", se enviará ademas, via email (a la casilla del administrador), el instructivo para realizar el enlace con AFIP, junto con el certificado de seguridad requerido por AFIP.

\\

Valores esperados: S o N.

\\
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fecha_inicio" type="string" required="false" %}
Fecha de inicio de actividades. Formato: dd/mm/aaaa
{% endswagger-parameter %}

{% swagger-parameter in="body" name="iibb" type="string" required="false" %}
El nro de ingresos brutos.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="iva_emails" type="string" required="false" %}
Las direcciones de email separadas por coma donde quieren recibir mensualmente el iva compras-ventas.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="iva_condicion" type="string" required="false" %}
La condición impositiva según tabla de referencia.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="direccion" type="string" required="false" %}
El domicilio fiscal. Dirección + número
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cuit" type="number" required="false" %}
Tu CUIT. Solo números.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="razon_social" type="string" required="false" %}
La razón social
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales actuales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales actuales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales actuales de acceso.
{% endswagger-parameter %}
{% endswagger %}

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

## Predeterminar CUIT + Punto de venta

Mediante éste método, podrás marcar como predeterminado el punto de venta, desde el cual estas realizando la solicitud.

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/puntos_venta/predeterminar" method="post" summary="Predeterminar CUIT + Punto de venta" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso

\\
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
	"error": "N",
	"errores": [] 
}
```
{% endswagger-response %}
{% endswagger %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"JHJKHJHJKHJK",
    "apitoken":"HJKHJHJKHKJHK",
    "apikey":"111" 
}
```
{% endcode %}

## Solicitar certificado de enlace con AFIP

Mediante éste método podrás obtener en la casilla de e-mail de los administradores de tu cuenta, un nuevo certificado de seguridad.

El certificado se generará para el CUIT desde el cual estas haciendo la solicitud.

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/puntos_venta/certificado" method="post" summary="Solicitar certificado" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"JHJKHJHJKHJK",
    "apitoken":"HJKHJHJKHKJHK",
    "apikey":"111" 
}
```
{% endcode %}
