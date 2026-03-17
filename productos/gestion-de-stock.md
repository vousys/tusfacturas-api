---
description: >-
  Simplifica la gestión de negocio y gestiona el stock con nuestra API para
  productos incluida en nuestra API para facturación AFIP
---

# Gestión de stock

### Administra el stock

Nuestra API ofrece endpoints para crear, leer y eliminar movimientos de stock. Integra nuestra solución a tu aplicación y accede a funcionalidades como consulta de stock en tiempo real, generación de reportes y gestión de alertas de bajo stock desde nuestra plataforma web. Conoce más sobre cómo se realizar la [gestión de stock](https://www.tusfacturas.app/caracteristicas-de-tus-facturas-electronica-stock.html).&#x20;

{% hint style="info" %}
### ¿Qué debes tener en cuenta?



* El código de producto debe ser único dentro de la lista de precios, sin embargo no realizamos ningúna válidación de nuestro lado con relación a ésto.
* El método es el mismo tanto para el alta de unidades al stock, como para la baja de unidades. Se utliza el campo "operacion" para distinguirlo.
* Podes enviar hasta 50 productos por request.


{% endhint %}

### Endpoint

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`productos/stock`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

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
