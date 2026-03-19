---
description: Mediante éste reporte obtendrás un listado con los saldos de tus clientes.
---

# Reporte: ¿Quién me debe? - Saldos

Mediante éste método podrás obtener un listado con los saldos de tus clientes.

### Endpoint

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`reportes/quienmedebe-saldos`</mark>

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
| limite           | number | Cantidad de registros por pagina.  Maximo valor esperado 1000 por página.                                                                                                          |
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
				"razon_social": "XXXXXXYYYY",
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
			"saldo": "$ 165,75"
		},
		{
			"cliente": {
				"razon_social": "XXXXX",
				"nombre_fantasia": "",
				"documento": {
					"tipo": "DNI",
					"nro": 1111111
				},
				"contacto": {
					"telefono": "",
					"whatsapp": "",
					"email": ""
				},
				"email": "XXXXX"
			},
			"saldo": "$ 36.830,00"
		}
	]
}
```
