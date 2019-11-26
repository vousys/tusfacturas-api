---
description: Consulta de información relacionada con tu cuenta
---

# Mi Cuenta

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="/v2/micuenta/consumo" %}
{% api-method-summary %}
Consultá el consumo de tu cuenta
{% endapi-method-summary %}

{% api-method-description %}
Éste método te brindara que cantidad de comprobantes podes emitir en el mes en curso, cuantos tenés programados como abono, y cuantos te quedan disponibles.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus Credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code title="JSON" %}
```
{
"error":"N",
"errores":[],
"abonos_pendientes":21,
"comprobantes_generados":12,
"comprobantes_cupo":100,
"comprobantes_disponibles": 79
}
```
{% endcode %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```text
{
   "usertoken":"JHJKHJHJKHJK",
    "apitoken":"HJKHJHJKHKJHK",
    "apikey":"111" 
}

```
{% endcode %}

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="/v2/micuenta/iva\_compras\_ventas" %}
{% api-method-summary %}
Solicitá el IVA Compras - Ventas
{% endapi-method-summary %}

{% api-method-description %}
Mediante éste método, solicitarás el envío del reporte IVA compras-ventas a una casilla de e-mail determinada. Se permite 1 casilla solamente por solicitud.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="anio" type="number" required=true %}
El año del período que se consulta.
{% endapi-method-parameter %}

{% api-method-parameter name="mes" type="number" required=true %}
El mes del período que se consulta.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
La dirección de e-mail a donde se enviará el reporte
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso  
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
La respuesta es error = S o error = N
{% endapi-method-response-example-description %}

{% code title="JSON" %}
```
{
"error":"N",
"errores":[]
}
```
{% endcode %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```text
{
"usertoken" :  "5ef7asdasdadsaa1b88fcabba3f",
"apikey"    :  "13562",
"apitoken"  :  "7668aadas21321adasdiaddaa6",
"mes": 11,
"anio": 2018,
"email": "tumail@dominio.com"

}

```
{% endcode %}

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="/v2/puntos\_venta/administrar" %}
{% api-method-summary %}
Administrar CUIT + Punto de venta
{% endapi-method-summary %}

{% api-method-description %}
Mediante éste método podrás crear nuevos puntos de venta o modificar el punto de venta enviado y recibir el instructivo para el enlace con AFIP \(según corresponda\).  
  
**Comentarios para modificación de puntos de venta:**  
- En el caso de la modificación del punto de venta, deberás realizar la solicitud con las keys del punto de venta  que querés modificar.  
- Ten en cuenta que aquellos puntos de venta que ya posean comprobantes, no podrán modificar su número de CUIT, condición impositiva ni de punto de venta.  
  
**Comentarios para el alta de puntos de venta:**  
- Si das de alta un punto de venta de un CUIT que ya existía y emitía factura electrónica, automáticamente éste quedará habilitado para emitir factura electrónica AFIP, sin requerir cargar en AFIP un nuevo certificado de seguridad. Lo único que deberás hacer en AFIP, es dar de alta el nuevo punto de venta de tipo "webservices".  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="operacion" type="string" required=true %}
Valores esperados: A  o M   
A = Alta de nuevo punto de venta   
M = Modifica el punto de venta, correspondiente a las apikey desde las cuales estoy enviando para hacer el request.
{% endapi-method-parameter %}

{% api-method-parameter name="conceptos\_tipo" type="string" required=true %}
Debe indicar el tipo de conceptos que factura, los cuales pueden ser:  
P = Productos   
PS = Productos y Servicios  
S = Servicios
{% endapi-method-parameter %}

{% api-method-parameter name="es\_predeterminado" type="string" required=true %}
Indica si el CUIT + Punto de venta es el predeterminado. Valores esperados: S o N
{% endapi-method-parameter %}

{% api-method-parameter name="esta\_activo" type="string" required=true %}
Indica si el CUIT + Punto de venta se encuentra activo y disponible para generar comprobantes. Valores esperados: S o N
{% endapi-method-parameter %}

{% api-method-parameter name="mercadopago" type="object" required=false %}
Según objeto "mercadopago" que se detalla abajo.
{% endapi-method-parameter %}

{% api-method-parameter name="xero" type="object" required=false %}
Según objeto "xero" que se detalla abajo.
{% endapi-method-parameter %}

{% api-method-parameter name="es\_agente\_retencion" type="string" required=true %}
Indica si el punto de venta es agente de retención. Valores esperados: S o N.
{% endapi-method-parameter %}

{% api-method-parameter name="factura" type="object" required=true %}
Un objeto del tipo "factura" según se detalla abajo.
{% endapi-method-parameter %}

{% api-method-parameter name="punto\_venta" type="number" required=true %}
El número del punto de venta a crear.   
Ej: 4
{% endapi-method-parameter %}

{% api-method-parameter name="factura\_afip" type="string" required=true %}
Indica si va a querer emitir factura electrónica AFIP.  En el caso que la respuesta sea "S", se enviará ademas, via email \(a la casilla del administrador\), el instructivo para realizar el enlace con AFIP, junto con el certificado de seguridad requerido por AFIP.  
Valores esperados: S o N.  
{% endapi-method-parameter %}

{% api-method-parameter name="fecha\_inicio" type="string" required=true %}
Fecha de inicio de actividades. Formato: dd/mm/aaaa
{% endapi-method-parameter %}

{% api-method-parameter name="iibb" type="string" required=true %}
El nro de ingresos brutos.
{% endapi-method-parameter %}

{% api-method-parameter name="iva\_emails" type="string" required=false %}
Las direcciones de email separadas por coma donde quieren recibir mensualmente el iva compras-ventas.
{% endapi-method-parameter %}

{% api-method-parameter name="iva\_condicion" type="string" required=true %}
La condición impositiva según tabla de referencia. 
{% endapi-method-parameter %}

{% api-method-parameter name="direccion" type="string" required=true %}
El domicilio fiscal. Dirección + número
{% endapi-method-parameter %}

{% api-method-parameter name="cuit" type="number" required=true %}
Tu CUIT. Solo números.
{% endapi-method-parameter %}

{% api-method-parameter name="razon\_social" type="string" required=true %}
La razón social
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales actuales de acceso.
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales actuales de acceso.
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales actuales de acceso.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Retorna todos los datos asociados al punto de venta.  
{% endapi-method-response-example-description %}

```
{
	"error": "N",
	"errores": [],
	"envio_instructivo": "N",
	"apikey": 123,
	"apitoken": "KSKJSJSHHAHHSGSGGSA",
	"usertoken": "SJDSHJADGHSAJDHSG"
}

En caso de detectar errores, se devolverá la variable error en "S" 
y dentro de errores, los diferentes mensajes enviados.P
Ej:

{
	"error": "S",
	"errores": ["Se han encontrado los siguientes errores:El cuit ingresado 2112321321 no es v\u00e1lido "],
	"apikey": "",
	"apitoken": "",
	"usertoken": "",
	"envio_instructivo": "N"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Objeto "mercadopago"

| Campo a enviar | Descripción |
| :--- | :--- |
| api\_key | La API KEY obtenida desde MercadoPago. |
| api\_secret | La API SECRET obtenieda desde MercadoPago. |

#### Objeto "xero"

| Campo a enviar | Descripción |
| :--- | :--- |
| habilitado | Indica si se encuentra habilitado o no. Valores esperados: S o N |
| consumer\_key | La consumer KEY obtenida desde XERO |
| shared\_secret | La shared\_secret obtenida desde XERO |
| habilitado\_web | Indica si se encuentra habilitado para sincronizar con XERO cuando se emiten comprobantes desde la plataforma web. Valores esperados: S o N |
| habilitado\_api | Indica si se encuentra habilitado para sincronizar con XERO cuando se emiten comprobantes desde la API. Valores esperados: S o N |

#### Objeto "factura"

| Campo a enviar | Descripcion |
| :--- | :--- |
| leyenda\_general\_predeterminada | Una leyenda predeterminada que saldrá impresa en todos los comprobantes que emitas. |
| titulo | El titulo que saldrá como encabezado de la factura. En gral se usa la razón social o el nombre de fantasía de la empresa. Máx de caracteres permitidos: 18 |
| subtitulo | El subtitulo que saldrá en el encabezado de la factura, bajo el titulo principal. Máx de caracteres permitidos: 18 |
| reply\_to\_email | La dirección de email para los reply-to en cada envío de comprobante. |
| reply\_to | El nombre de quien envía los comprobantes. |
| mensaje | El mensaje predeterminado que saldrá en el envío de cada comprobante. |
| copias | La cantidad de copias que se generan dentro del PDF. Valores esperados:  2= para recibir original y duplicado, 3= para recibir original, duplicado y triplicado |
| cbu | Opcional: El número del CBU. Campo numérico, maximo 30 dígitos. |

#### JSON De ejemplo a enviar

{% code title="JSON" %}
```text
{
   "usertoken":"JHJKHJHJKHJK",
    "apitoken":"HJKHJHJKHKJHK",
    "apikey":"111",
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



{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="/v2/puntos\_venta/predeterminar" %}
{% api-method-summary %}
Predeterminar CUIT + Punto de venta
{% endapi-method-summary %}

{% api-method-description %}
Marca como predeterminado el punto de venta desde el cual estoy realizando la solicitud.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso  
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
	"error": "N",
	"errores": [] 
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```text
{
   "usertoken":"JHJKHJHJKHJK",
    "apitoken":"HJKHJHJKHKJHK",
    "apikey":"111" 
}

```
{% endcode %}

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="/v2/puntos\_venta/certificado" %}
{% api-method-summary %}
Solicitar certificado
{% endapi-method-summary %}

{% api-method-description %}
Mediante éste método podrás obtener en la casilla de e-mail de los administradores de tu cuenta, un nuevo certificado de seguridad.  
El certificado se generará para el  CUIT desde el cual estas haciendo la solicitud.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```text
{
   "usertoken":"JHJKHJHJKHJK",
    "apitoken":"HJKHJHJKHKJHK",
    "apikey":"111" 
}

```
{% endcode %}







