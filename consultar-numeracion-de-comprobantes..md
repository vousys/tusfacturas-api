---
description: >-
  Mediante éste método podrás consultar la próxima numeración de un tipo de
  comprobante.
---

# Consultar numeración de comprobantes.

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api" path="/v2/facturacion/numeracion" %}
{% api-method-summary %}
Consultar numeración
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter required=true name="comprobante" %}
**tipo**    Campo numérico según tabla de referencia de Tipos de comprobantes\(\*\*\*\). Ejemplo: FACTURA B **operacion**    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V   
**punto\_venta**    Campo numérico entero. Longitud máxima 4 digitos. Ejemplo: 3
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso.
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso  
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de detectar algún error, el campo error, se devuelve con una "S" y dentro de "errores" se devolverá una lista con cada uno de los mensajes.  
  
Importante: Los campos número y punto de venta, se retornan como numéricos  
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
	"comprobante": {
		"tipo": "NOTA DE DEBITO B",
		"operacion": "V",
		"punto_venta": 2,
		"numero": 6
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON a enviar para consultar la numeración del próximo comprobante.

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
	"usertoken": "jajajja8c8bf67c884e1405e26c03c85",
	"apikey": "9991",
	"apitoken": "kkakak208a17cdfc4e4741437baddaa6",
	"comprobante": {
		"tipo": "NOTA DE DEBITO B",
		"operacion": "V",
		"punto_venta": "2"
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Estructura de datos 

| `tipo` | Campo numérico según tabla de referencia de [Tipos de comprobantes\(\*\*\*\)](https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes). **Ejemplo: FACTURA B** |
| --- | --- | --- |
| `operacion` | Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\).  Valores Permitidos: **V, C** **Ejemplo: V** |
| `punto_venta` | Campo numérico entero. Longitud máxima 4 digitos. **Ejemplo: 3** |

