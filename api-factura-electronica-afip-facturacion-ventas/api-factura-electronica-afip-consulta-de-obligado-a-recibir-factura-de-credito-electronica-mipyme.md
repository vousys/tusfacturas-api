---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para consultar
  si tu cliente está obligado a recibir comprobantes de tipo Factura de Crédito
  electrónica MiPyme.
---

# Consulta para verificar si estoy obligado a recibir o emitir Factura de Crédito electrónica MiPyme

{% hint style="info" %}
El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso.

IMPORTANTE: Para poder realizar ésta consulta, deberás tener agregado en tu cuenta AFIP, el servicio de "**Webservice Registro de Facturas de Crédito Electrónica MiPyMEs "** . Te indicamos cómo hacerlo en el [instructivo de integración con AFIP : Paso 6](https://youtu.be/\_YSRksd0\_A0)
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app" path="/api/v2/facturacion/requiere_fec" method="post" summary="Consulta de obligado a recibir MiPyme" %}
{% swagger-description %}
Éste método te devolverá si tu cliente se encuentra obligado a recibir facturas de tipo MiPyme y a partir de que monto se encuentra obligado.
{% endswagger-description %}

{% swagger-parameter in="body" name="fecha" type="string" required="false" %}
La fechad de emisión del comprobante en cuestión. Formato esperado: dd/mm/aaaa
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cuit" type="number" required="false" %}
El CUIT de tu cliente. Campo numérico de 11 digitos
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="number" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso

\\
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
{% code title="JSON" %}
```
En caso de no encontrar errores obtendrás una respuesta 
como la siguiente:

{
	"error": "N",
	"errores": [],
	"rta": "",
	"esta_obligado": "S",
	"importe_desde": 100000
}

En caso de detectar errores, obtendrás una respuesta 
como la siguiente:

{
	"error": "S",
	"errores": ["El CUIT enviado INF es invalido."],
	"rta": "", 
}





```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar:

```
{
	"apitoken": "xxxx",
	"apikey": xxxx,
	"usertoken": "xxxx",
	"cuit": 12345678901,
	"fecha": "08/12/2019"
}
```

### Ejemplo del JSON de respuesta:

```
En caso de éxito:

{
	"error": "N",
	"errores": [],
	"rta": "",
	"esta_obligado": "S",
	"importe_desde": 100000
}

En caso de detectar errores:

{
	"error": "S",
	"errores": ["El CUIT enviado INF es invalido."],
	"rta": "", 
}
```
