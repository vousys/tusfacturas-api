---
description: >-
  TusFacturasAPP: ¡Más que facturas! Gestiona tus cobros, actualiza saldos y
  optimiza tu flujo de caja con nuestra API para generar recibos de cobro.
---

# Ingresar pago a un comprobante emitido

{% hint style="info" %}
Los cobros que informes, se usan solo para la gestión interna de nuestra plataforma y tu cliente no lo verá reflejado en el PDF del comprobante que emitiste, ya que el único objetivo que tiene éste bloque es nutrir la cuenta corriente de tu cliente, con el pago realizado.
{% endhint %}

## Datos a tener en cuenta

{% hint style="info" %}
* **NO** podrás enviar los siguientes medios de pago: "cheques" y ni "retenciones"..
* Se realizara una validación del total que se indique, contra la sumatoria de los medios de pago detallados
* El total de los pagos **NO** debe superar el importe total del comprobante, pero si puede ser inferior, para indicar que el comprobante recibió un pago parcial.
{% endhint %}

## Ingresar pagos a un comprobante emitido

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`pagar`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción



#### Request Body

| Name        | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| apitoken    | String | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| apikey      | String | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| usertoken   | String | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| comprobante | object | <p>Un objeto compuesto de los siguientes atributos: </p><p><strong>tipo:</strong> Campo alfanumérico. Longitud máx: 50 caracteres, conteniendo el tipo de comprobante a consultar. Ej: FACTURA A </p><p><strong>operacion :</strong> Campo alfanumérico. Longitud máx: 1 carácter. Valores permitidos (V o C) ya sea para ventas o compras.</p><p><strong>punto_venta</strong> Campo númerico para indicar el número del punto de venta.</p><p><strong>numero :</strong> Campo numérico. Longitud máx: 8. Indica el número del comprobante a consultar.</p><p><strong>pagos</strong>: Bloque según estructura que se detalla a continuación</p><p></p> |

{% tabs %}
{% tab title="200: OK " %}
Ejemplos de las respuestas JSON en caso de éxito o error

{% tabs %}
{% tab title="Exito" %}
```
{
	"error": "N",
	"errores": [""],
}
```
{% endtab %}

{% tab title="Con errores" %}
```
{
	"error": "S",
	"errores": 
			"Error 2"],
}
```
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

## Ejemplo del JSON completo a enviar

```
{
	"apitoken": "xxxx",
	"apikey": xxxx,
	"usertoken": "xxxx",
	 
	"comprobante": 
	{
		"tipo": "FACTURA A",
		"operacion": "V",
		"punto_venta": "00010",
		"numero": "00000109", 
		"pagos" : 
		      {
			"formas_pago" : [ 
				{"descripcion" : "VISA", "importe" : 200},
				{"descripcion" : "MercadoPago", "importe" : 1000}				
					], 
			"total": 1200
			}
	}
}
 
```

### Estructura del objeto "comprobante

| Nombre del campo | Tipo de dato                                                                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| tipo             | <p>Campo numérico según tabla de referencia de Tipos de comprobantes(***).</p><p>Ejemplo: FACTURA B</p>                                           |
| punto\_venta     | <p>Campo numérico entero.</p><p>Longitud máxima 5 dígitos.</p><p>Ejemplo: 3</p>                                                                   |
| numero           | <p>Campo numérico entero.</p><p>Longitud máxima 8 digitos.</p>                                                                                    |
| operacion        | <p>Campo alfanumérico.</p><p>Longitud 1 carácter.</p><p>Indica si envía una factura de venta (V) o de compra (C).</p><p>Valores Permitidos: V</p> |
| pagos            | Según estructura que se detalla a continuación                                                                                                    |

```
{
	  
	"comprobante": 
	{
		"tipo": "FACTURA A",
		"operacion": "V",
		"punto_venta": "00010",
		"numero": "00000109", 
		"pagos" : { .... }
	}
}
```

### Estructura del objeto pagos

| nombre del campo | Requerido | Detalle                                                                                                  |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| formas\_pago     | SI        | array con multiples items, según estructura que se detalla a continuación                                |
| total            | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p> |

Información de los campos que componen el **array de pagos > formas\_pago**

| nombre del campo | Requerido | Detalle                                                                                                                                                                                              |
| ---------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| descripcion      | SI        | <p>El nombre del medio de pago elegido para cancelar el comprobante. 255 caracteres max.</p><p>En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente.</p> |
| importe          | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                                             |

Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "pagos" : 
   {
	"formas_pago" : [ 
			{"descripcion" : "VISA DB", "importe" : 0.6},
			{"descripcion" : "MercadoPago", "importe" : 50}
			], 
	"total": 50.6
   }, 
 }
```
{% endcode %}

## Ejemplo del JSON completo a enviar

```
{
	"apitoken": "xxxx",
	"apikey": xxxx,
	"usertoken": "xxx",
	 
	"comprobante": 
	{
		"tipo": "FACTURA A",
		"operacion": "V",
		"punto_venta": "00010",
		"numero": "00000109", 
		"pagos" : 
		      {
			"formas_pago" : [ 
				{"descripcion" : "VISA", "importe" : 200},
				{"descripcion" : "MercadoPago", "importe" : 1000}				
					], 
			"total": 1200
			}
	}
}
 
```
