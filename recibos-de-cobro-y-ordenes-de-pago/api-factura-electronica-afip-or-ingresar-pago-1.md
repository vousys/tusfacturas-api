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

### Generar recibos de cobro

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/caja/`<mark style="color:purple;">`nuevo`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.



#### Request Body

| Name               | Type   | Description                                                                                                                                                                                                               |
| ------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| apitoken           | String | Tus credenciales de acceso                                                                                                                                                                                                |
| apikey             | String | Tus credenciales de acceso                                                                                                                                                                                                |
| usertoken          | String | Tus credenciales de acceso                                                                                                                                                                                                |
| tipo               | string | Deberás enviar el valor "RC"                                                                                                                                                                                              |
| fecha              | string | Campo en formato fecha dd/mm/aaaa que indica la fecha en que llevará el recibo de cobro                                                                                                                                   |
| cuenta\_principal  | string | Campo alfanumérico de hasta 255 caracteres. El nombre de la cuenta principal a la que aplicarás éste recibo de cobro. La misma debe existir en los parámetros de tu espacio de trabajo.                                   |
| cuenta\_secundaria | string | Campo alfanumérico de hasta 255 caracteres. El nombre de la cuenta secundaria (relacionada con la principal) a la que aplicarás éste recibo de cobro. La misma debe existir en los parámetros de tu espacio de trabajo.   |
| comentario         | string | OPCIONAL. Campo alfanumérico de hasta 255 caracteres, que quedará registrado como un comentario interno                                                                                                                   |
| leyenda            | string | OPCIONAL. Campo alfanumérico de hasta 255 caracteres, que quedará registrado como leyenda y saldrá impreso en el PDF del recibo, en caso que desees generarlo.                                                            |
| pagos              | string | Según estructura que se detalla a continuación                                                                                                                                                                            |

{% hint style="info" %}
## Datos a tener en cuenta

* **NO** podrás enviar los siguientes medios de pago: "cheques" y ni "retenciones".
* No podrás usar éste método para generar recibos de cobro por facturas emitidas. Para eso debes usar el método de "[Ingresar pago a un comprobante emitido](api-factura-electronica-afip-or-ingresar-pago-1.md#ingresar-pagos-a-un-comprobante-emitido)"
* Se realizara una validación del total que se indique, contra la sumatoria de los medios de pago detallados
{% endhint %}

### Ejemplo del JSON completo a enviar

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

### Respuesta JSON

```
{
	"error": "S",
	"errores":  ["Error 2"],
}
```

En caso de éxito:

```
{
	"error": "N",
	"errores": [],
}
```

