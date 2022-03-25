---
description: >-
  Mediante ésta función, podrás ingresar dinero asignado a diferentes planes de
  cuenta que existan en tu espacio de trabajo, e impacten en las diferentes
  cajas
---

# Generar un recibo de cobro

{% hint style="info" %}
Los cobros que informes, se usan solo para la gestión interna de nuestra plataforma y no podrás generar dentro de éste método, cobros por comprobantes que emitiste a tus clientes, para eso debes usar el método de "[Ingresar pago a un comprobante emitido](api-factura-electronica-afip-or-ingresar-pago-1.md#ingresar-pagos-a-un-comprobante-emitido)"
{% endhint %}

{% swagger method="post" path="/v2/caja/nuevo" baseUrl="https://www.tusfacturas.app/app/api" summary="Generar recibos de cobro" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="apitoken" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tipo" type="string" %}
Deberás enviar el valor "RC" 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fecha" type="string" %}
Campo en formato fecha dd/mm/aaaa que indica la fecha en que llevará el recibo de cobro
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cuenta_principal" type="string" %}
Campo alfanumérico de hasta 255 caracteres. El nombre de la cuenta principal a la que aplicarás éste recibo de cobro. La misma debe existir en los parámetros de tu espacio de trabajo.  
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cuenta_secundaria" type="string" %}
Campo alfanumérico de hasta 255 caracteres. El nombre de la cuenta secundaria (relacionada con la principal) a la que aplicarás éste recibo de cobro. La misma debe existir en los parámetros de tu espacio de trabajo.  
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comentario" type="string" %}
OPCIONAL. Campo alfanumérico de hasta 255 caracteres, que quedará registrado como un comentario interno
{% endswagger-parameter %}

{% swagger-parameter in="body" name="leyenda" type="string" %}
OPCIONAL. Campo alfanumérico de hasta 255 caracteres, que quedará registrado como leyenda y saldrá impreso en el PDF del recibo, en caso que desees generarlo.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pagos" type="string" %}
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

{% hint style="info" %}
* ## Datos a tener en cuenta
* **NO** podrás enviar los siguientes medios de pago: "cheques" y ni "retenciones".
* No podrás usar éste método para generar recibos de cobro por facturas emitidas. Para eso debes usar el método de "[Ingresar pago a un comprobante emitido](api-factura-electronica-afip-or-ingresar-pago-1.md#ingresar-pagos-a-un-comprobante-emitido)"
* Se realizara una validación del total que se indique, contra la sumatoria de los medios de pago detallados
{% endhint %}

## Ejemplo del JSON completo a enviar

```
{
	"apitoken": "xxxx",
	"apikey": xxxx,
	"usertoken": "xxxx", 
	"tipo": "RC",
	"fecha": "25/03/2022",
	"cuenta_principal": "Comisiones" ,
	"cuenta_secundaria": "Comisiones por ventas",
	"comentario": "",
	"leyenda": "",
	"pagos": { 			
				"formas_pago": [
					{"descripcion": "AMEX", "importe": "40"},
				  	{"descripcion": "VISA", "importe": "30"},
					{"descripcion": "efectivo", "importe": "5"},
					{"descripcion": "MasterCard", "importe": "30"}
					
					
				],
			 "total": 105
		} 
}
 
```

### Estructura del objeto pagos

| nombre del campo | Requerido | Detalle                                                                                                  |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| formas\_pago     | SI        | array con multiples items, según estructura que se detalla a continuación                                |
| total            | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p> |

Información de los campos que componen el **array de pagos > formas\_pago**

| nombre del campo | Requerido | Detalle                                                                                                                                                                  |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| descripcion      | SI        | <p>El nombre del medio de pago elegido . 255 caracteres max.</p><p>En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente.</p> |
| importe          | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                 |

Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
{
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
