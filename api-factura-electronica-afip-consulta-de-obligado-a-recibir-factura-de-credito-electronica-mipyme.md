---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para consultar
  si tu cliente está obligado a recibir comprobantes de tipo Factura de Crédito
  electrónica MiPyme.
---

# API Factura electrónica: Consulta de obligado a recibir Factura de Crédito electrónica MiPyme

{% hint style="info" %}
El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso.

IMPORTANTE: Para poder realizar ésta consulta,  deberás tener agregado en tu cuenta AFIP, el servicio de "**Webservice Registro de Facturas de Crédito Electrónica MiPyMEs "** . Te indicamos como hacerlo en el[ instructivo de integración con AFIP : Paso 6 ](https://www.tusfacturas.app/app/afip-como-enlazar-con-tusfacturas.html)
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.app/app" path="/api/v2/facturacion/requiere\_fec" %}
{% api-method-summary %}
Consulta de obligado a recibir MiPyme
{% endapi-method-summary %}

{% api-method-description %}
Éste método te devolverá si tu cliente se encuentra obligado a recibir facturas de tipo MiPyme y a partir de que monto se encuentra obligado.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="fecha" type="string" required=true %}
La fechad de emisión del comprobante en cuestión. Formato esperado: dd/mm/aaaa
{% endapi-method-parameter %}

{% api-method-parameter name="cuit" type="number" required=true %}
El CUIT de tu cliente. Campo numérico de 11 digitos
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="number" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso  
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON a enviar

```text
{
	"apitoken": "asdadasd123",
	"apikey": 0001,
	"usertoken": "asdasdasd123",
	"cuit": 12345678901,
	"fecha": "08/12/2019"
}
```



