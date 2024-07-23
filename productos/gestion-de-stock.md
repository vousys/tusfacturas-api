---
description: >-
  Gestiona el stock de tus productos con facilidad y eficiencia con nuestra API
  de productos.
---

# Gestión de stock

## Administrá el stock

Éste método te permite enviar un lote de hasta 50 productos para consultar.

{% hint style="info" %}
### ¿Qué debes tener en cuenta?



* El código de producto debe ser único dentro de la lista de precios
* El método es el mismo tanto para el alta de unidades al stock, como para la baja de unidades. Se utliza el campo "operacion" para distinguirlo.
* Podes enviar hasta 50 productos por request.


{% endhint %}

### Request

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`productos/stock`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción



#### Request Body

| Name      | Type   | Description                                                                                    |
| --------- | ------ | ---------------------------------------------------------------------------------------------- |
| productos | array  | **Una lista de objetos "**[**producto**](gestion-de-stock.md#estructura-de-cada-producto)**"** |
| usertoken | string | Tus credenciales de acceso                                                                     |
| apikey    | string | Tus credenciales de acceso                                                                     |
| apitoken  | string | Tus credenciales de acceso                                                                     |
| operacion | string | Valores posibles:  "A" = Alta de unidades al stock ó "B" = "Baja de unidades al stock"         |

### Ejemplo del JSON que debes enviar

```
{
    "usertoken": "xxxx",
    "apikey": "xxxx",
    "apitoken": "xxxx",
    "operacion": "A",
    "productos": [
        {
            "lista_precios": "Trenes",
            "codigo": "tren10384",
            "cantidad": 140
        },
        {
            "lista_precios": "Camiones",
            "codigo": "Cam01",
            "cantidad": 30
        }
    ]
}
```



### ¿Qué te retorna en cada llamada?

Se devolverá una lista, en el mismo orden en que se recibió, conteniendo la siguiente estructura:

```
{
	"error": "N",
	"errores": [],
	"productos": [
		{
			"lista_precios": "Trenes",
			"codigo": "tren10384",
			"error": "S",
			"errores": [
				"No existen productos que afecten el stock con el codigo enviado:tren10384"
			]
		},
		{
			"codigo": "Cam01",
			"lista_precios": "Camiones",
			"stock_actual": 204,
			"stock_minimo": 500,
			"error": "N",
			"errores": []
		}
	]
}

```
