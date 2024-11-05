---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la
  numeración de tus comprobantes.
---

# Consultar numeración de comprobantes.

## Consultar numeración

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/numeracion`

💡 El uso de éste método no contabiliza como un request en tu suscripción

#### Request Body

| Name        | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| comprobante | Object | <p><strong>CAMPOS DEL OBJETO COMPROBANTE:</strong></p><p><strong>tipo</strong> Campo numérico según tabla de referencia de Tipos de comprobantes(***).</p><p>Ejemplo: FACTURA B</p><p><strong>operacion</strong> Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V<br><strong>punto_venta</strong> Campo numérico entero. Longitud máxima <strong>5</strong> digitos. Ejemplo: 3</p> |
| apikey      | string | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| apitoken    | string | Tus credenciales de acceso.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| usertoken   | string | <p>Tus credenciales de acceso</p><p></p>                                                                                                                                                                                                                                                                                                                                                                                                                                  |

{% tabs %}
{% tab title="200 " %}
En caso de detectar algún error, el campo error, se devuelve con una "S" y dentro de "errores" se devolverá una lista con cada uno de los mensajes.Importante: Los campos número y punto de venta, se retornan como numéricos

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
{% endtab %}
{% endtabs %}

### Ejemplo del JSON a enviar, para consultar la numeración del próximo comprobante.

{% code title="JSON" %}
```json
{
	"usertoken": "xxxxx",
	"apikey": "xxxxx",
	"apitoken": "xxxxx",
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
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |



### Ejemplo de JSON de respuesta

```json
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

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
