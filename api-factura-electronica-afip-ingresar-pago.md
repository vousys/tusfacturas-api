---
description: >-
  Mediante ésta función podrás ingresar pagos a cada comprobante que emítas, de
  modo que la cuenta corriente refleje no solo las ventas, sino los cobros que
  capturas desde tu plataforma.
---

# API Factura electrónica AFIP - Ingresar pago

{% swagger method="post" path="/v2/facturacion/pagar" baseUrl="https://www.tusfacturas.app/app/api" summary="Ingresar pagos a un comprobante emitido" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apitoken" required="true" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" required="true" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" required="true" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" type="object" required="true" %}
Según estructura que se detalla a continuación


{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
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
{% endswagger-response %}
{% endswagger %}

### Estructura de comprobante

| Nombre del campo | Tipo de dato                                                                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tipo             | <p>Campo numérico según tabla de referencia de Tipos de comprobantes(***). </p><p>Ejemplo: FACTURA B</p>                                                |
| punto\_venta     | <p>Campo numérico entero. </p><p>Longitud máxima 5 dígitos. </p><p>Ejemplo: 3</p>                                                                       |
| numero           | <p>Campo numérico entero. </p><p>Longitud máxima 8 digitos. </p>                                                                                        |
| operacion        | <p>Campo alfanumérico. </p><p>Longitud 1 carácter. </p><p>Indica si envía una factura de venta (V) o de compra (C). </p><p>Valores Permitidos: V   </p> |
| pagos            | Según estructura que se detalla a continuación                                                                                                          |

### Estructura de pagos&#x20;

Los pagos que informes, se usan solo para la gestión interna de nuestra plataforma y tu cliente no lo verá reflejado en el PDF del comprobante que emitiste, ya que el único objetivo que tiene éste bloque es nutrir la cuenta corriente de tu cliente, con el pago realizado.

{% hint style="info" %}
Cosas a tener en cuenta:&#x20;

* **NO** podrás enviar los siguientes medios de pago: cheques y detalle de retenciones.
* Se realizara una validación del total que se indique, contra la sumatoria de los medios de pago detallados
* El total de los pagos **NO** debe superar el importe total del comprobante, pero si puede ser inferior, para indicar que el comprobante recibió un pago parcial.
{% endhint %}

&#x20;Información de los campos que componen el **bloque "pagos"**

| nombre del campo | Requerido | Detalle                                                                                                  |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| formas\_pago     | SI        | array con multiples items, según estructura que se detalla a continuación                                |
| total            | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p> |

Información de los campos que componen el **array de pagos > formas\_pago**&#x20;

| nombre del campo | Requerido | Detalle                                                                                                                                                                                 |
| ---------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| descripcion      | SI        | El nombre del medio de pago elegido para cancelar el comprobante. 255 caracteres max. En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente. |
| importe          | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                                |

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
	"apitoken": "asdadsadasdada",
	"apikey": 10000,
	"usertoken": "asdadasdadsasd",
	 
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
