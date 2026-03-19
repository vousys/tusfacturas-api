---
description: >-
  Mediante éste reporte obtendrás un listado con el detalle de las deudas de tus
  clientes.
---

# Reporte: ¿Quién me debe? - Detalle

Mediante este método podrás obtener un listado detallado de las deudas de tus clientes. La información se encuentra paginada en bloques de 100 clientes y contempla hasta 500 conceptos adeudados por cliente, al día de la fecha.

Debido a que la gestión de cuentas corrientes es por cliente y centraliza la recepción de comprobantes de todos los puntos de venta, el reporte consolidará la información total, independientemente de las credenciales utilizadas para su solicitud.

### Endpoint

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`reportes/quienmedebe-detalle`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

| Name             | Type   | Description                                                                                                                                                                        |
| ---------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| saldos\_a\_favor | string | Indica con "SI" o con "NO", si el reporte deberá incluir aquellos clientes que tengan saldo a favor (menor a cero)                                                                 |
| cf\_sin\_dni     | string | Indica con "SI" o con "NO", si el reporte deberá incluir aquellas ventas a clientes consumidores finales que no tengan especificado su tipo y nro de documento.                    |
| saldos\_mayor\_a | number | En caso que quieras obtener el reporte de aquellos clientes cuyo saldo sea mayor a un valor x, deberas enviar éste valor.  Ej:  100.50 ( 2 decimales max - punto separa decimales) |
| apikey           | string | Tus credenciales de acceso                                                                                                                                                         |
| apitoken         | string | Tus credenciales de acceso                                                                                                                                                         |
| usertoken        | string | Tus credenciales de acceso                                                                                                                                                         |
| limite           | number | Cantidad de registros por pagina.  Maximo valor esperado 100 por página.                                                                                                           |
| pagina           | number | Nro de paginación. Inicia en cero (0).                                                                                                                                             |

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"saldos_a_favor": "NO", 
"cf_sin_dni": "NO",
"saldos_mayor_a":"0",
"limite": 2,
"pagina": 0

}
```
{% endcode %}

#### Ejemplo del JSON de respuesta

```
{
	"rta": "OK",
	"error": "N",
	"total": 241,
	"errores": [],
	"reporte": [
		{
			"cliente": {
				"razon_social": "xxxxxxyyyy",
				"nombre_fantasia": "",
				"documento": {
					"tipo": "DNI",
					"nro": 22222222
				},
				"contacto": {
					"telefono": "",
					"whatsapp": "",
					"email": ""
				},
				"email": ""
			},
			"saldo": "$ 165,75",
			"detalle": [
				{
					"fecha": "18/06/2025",
					"importe_adeudado": "$ 165,75",
					"concepto": "FACTURA B 00010-00009462 (xxxxxx)",
					"vencimiento": "18/06/2025 ",
					"estado_vencimiento": "274 DIAS ATRASO"
				}
			]
		},
		{
			"cliente": {
				"razon_social": "xxxxxxxx",
				"nombre_fantasia": "",
				"documento": {
					"tipo": "DNI",
					"nro": 22222222
				},
				"contacto": {
					"telefono": "",
					"whatsapp": "",
					"email": ""
				},
				"email": ""
			},
			"saldo": "$ 36.830,00",
			"detalle": [
				{
					"fecha": "06/06/2024",
					"importe_adeudado": "$ 36.830,00",
					"concepto": "FACTURA B 00010-00005138 (xxxx)",
					"vencimiento": "06/06/2024 ",
					"estado_vencimiento": "651 DIAS ATRASO"
				}
			]
		}
	]
}
```
