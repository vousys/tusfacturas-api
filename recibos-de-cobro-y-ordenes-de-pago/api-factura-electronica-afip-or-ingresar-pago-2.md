---
description: >-
  Mediante ésta función, podrás generar órdenes de pago, asignado a diferentes
  planes de cuenta que existan en tu espacio de trabajo, e impacten en las
  diferentes cajas.
---

# Generar una orden de pago

{% hint style="info" %}
Las órdenes de pago que informes, se usan solo para la gestión interna de nuestra plataforma y no podrás generar dentro de éste método, órdenes de pago por comprobantes que tus proveedores te emitieron.
{% endhint %}

## Generar órdenes de pago&#x20;

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/caja/`<mark style="color:purple;">`nuevo`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción



#### Request Body

| Name               | Type   | Description                                                                                                                                                                                                               |
| ------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| apitoken           | String | Tus credenciales de acceso                                                                                                                                                                                                |
| apikey             | String | Tus credenciales de acceso                                                                                                                                                                                                |
| usertoken          | String | Tus credenciales de acceso                                                                                                                                                                                                |
| tipo               | string | Deberás enviar el valor "OP"                                                                                                                                                                                              |
| fecha              | string | Campo en formato fecha dd/mm/aaaa que indica la fecha en que llevará el recibo de cobro                                                                                                                                   |
| cuenta\_principal  | string | Campo alfanumérico de hasta 255 caracteres. El nombre de la cuenta principal a la que aplicarás éste recibo de cobro. La misma debe existir en los parámetros de tu espacio de trabajo.                                   |
| cuenta\_secundaria | string | Campo alfanumérico de hasta 255 caracteres. El nombre de la cuenta secundaria (relacionada con la principal) a la que aplicarás éste recibo de cobro. La misma debe existir en los parámetros de tu espacio de trabajo.   |
| comentario         | string | OPCIONAL. Campo alfanumérico de hasta 255 caracteres, que quedará registrado como un comentario interno                                                                                                                   |
| leyenda            | string | OPCIONAL. Campo alfanumérico de hasta 255 caracteres, que quedará registrado como leyenda y saldrá impreso en el PDF del recibo, en caso que desees generarlo.                                                            |
| pagos              | string | Según estructura que se detalla a continuación                                                                                                                                                                            |

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

{% hint style="info" %}
* ## Datos a tener en cuenta
* **NO** podrás enviar los siguientes medios de pago: "cheques" y ni "retenciones".
* Se realizara una validación del total que se indique, contra la sumatoria de los medios de pago detallados
{% endhint %}

## Ejemplo del JSON completo a enviar

```
{
	"apitoken": "xxxx",
	"apikey": xxxx,
	"usertoken": "xxxx", 
	"tipo": "OP",
	"fecha": "25/03/2022",
	"cuenta_principal": "Gastos de oficina" ,
	"cuenta_secundaria": "Moviliario",
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

| nombre del campo | Requerido | Detalle                                                                                                                                                                 |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| descripcion      | SI        | <p>El nombre del medio de pago elegido. 255 caracteres max.</p><p>En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente.</p> |
| importe          | SI        | <p>Campo numérico con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                |

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
