---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la
  numeración de tus comprobantes.
---

# API Factura electrónica AFIP - Consultar numeración de comprobantes.

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/facturacion/numeracion" method="post" summary="Consultar numeración" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="comprobante" %}
**tipo**

    Campo numérico según tabla de referencia de Tipos de comprobantes(***). Ejemplo: FACTURA B 

**operacion**

    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V 

\




**punto_venta**

    Campo numérico entero. Longitud máxima 4 digitos. Ejemplo: 3
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso

\



{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de detectar algún error, el campo error, se devuelve con una "S" y dentro de "errores" se devolverá una lista con cada uno de los mensajes.

Importante: Los campos número y punto de venta, se retornan como numéricos
" %}
{% code title="JSON" %}
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
{% endcode %}
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar para consultar la numeración del próximo comprobante.

{% code title="JSON" %}
```
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
{% endcode %}

### Estructura de datos 

| `tipo`        | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). <br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                  |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
