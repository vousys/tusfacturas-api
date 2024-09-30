---
description: >-
  Gestiona tus productos con facilidad y eficiencia con nuestra API de
  productos, incluida en nuestra API para facturación AFIP.
---

# Administrar productos

## Agregá o modificá productos

Éste método te permite enviar un lote de hasta 50 productos ya sea para darlos de alta o para modificarlos.&#x20;

{% hint style="info" %}
### ¿Qué debes tener en cuenta?



* El código de producto debe ser único dentro de la lista de precios
* Al modificar un producto, se utilizará como clave de búsqueda el campo "codigo" +  "lista de precios"
* Podes enviar hasta 50 productos por request.
* El JSON a enviar es el mismo tanto para el alta como para la modificación, solo se debe  cambiar el valor del campo "operacion".
* stock\_actual: Éste campo solo será utilizado en el alta del producto, cuando el campo  "afecta\_stock" = "S".  Luego de crear el producto se incorporarán al stock las unidades indicadas.
{% endhint %}

### Request

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`productos/administrar`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.



#### Request Body

| Name      | Type   | Description                                                                                         |
| --------- | ------ | --------------------------------------------------------------------------------------------------- |
| productos | array  | **Una lista de objetos "**[**producto**](administrar-productos.md#estructura-de-cada-producto)**"** |
| usertoken | string | Tus credenciales de acceso                                                                          |
| apikey    | string | Tus credenciales de acceso                                                                          |
| apitoken  | string | Tus credenciales de acceso                                                                          |
| operacion | string | Valores posibles: "A" para agregar nuevos productos o "M" para modificar productos                  |

### Ejemplo del JSON que debes enviar

<pre><code>{
    "usertoken": "xxxx",
    "apikey": "xxxx",
    "apitoken": "xxxx",
    "operacion": "A",
<strong>    "productos": [
</strong>        {
            "descripcion": "Tren de carga P#1",
            "unidad_bulto": "1",
            "lista_precios": "Trenes",
            "codigo": "tren10384",
            "precio_unitario_sin_iva": 1000,
            "alicuota": 21,
            "impuestos_internos_alicuota": 0,
            "moneda": "DOL",
            "codbar": "123213213213",
            "rg5329": "S",
            "unidad_medida": "7",
            "afecta_stock": "N",
            "stock_actual": 0,
            "stock_minimo": 100
        },
        {
            "descripcion": "Camion de arena",
            "unidad_bulto": "1",
            "lista_precios": "Camiones",
            "codigo": "Cam01",
            "precio_unitario_sin_iva": 1000,
            "alicuota": 21,
            "moneda": "PES",
            "codbar": "",
            "impuestos_internos_alicuota": 45,
            "unidad_medida": "7",
            "afecta_stock": "S",
            "stock_actual": 154,
            "stock_minimo": 500
        }
    ]
}
</code></pre>

### Estructura de cada "producto"

<table data-header-hidden><thead><tr><th></th><th></th><th data-type="checkbox">¿Requerido?</th></tr></thead><tbody><tr><td><code>descripcion</code></td><td>Campo alfanumerico de hasta 255 caracteres.</td><td>true</td></tr><tr><td><code>codigo</code></td><td>Campo alfanumerico de hasta 50 caracteres.</td><td>true</td></tr><tr><td>lista_precios</td><td>Campo alfanumerico de hasta 255 caracteres.</td><td>true</td></tr><tr><td>unidad_bulto</td><td>Valor nlumerico entero.</td><td>true</td></tr><tr><td>precio_unitario_sin_iva</td><td>Valor numerico con hasta 3 decimales. Separador de decimales: punto</td><td>true</td></tr><tr><td>alicuota</td><td>Valor según tabla de referencia: "<a href="../parametros/tablas-de-referencia.md#alicuotas-de-iva">Alicuotas</a>" </td><td>true</td></tr><tr><td>moneda</td><td>Valores posibles: "PES" para indicar "Pesos argentinos" o "DOL" para indicar "Dolares"</td><td>true</td></tr><tr><td>codbar</td><td>Campo alfanumerico de hasta 255 caracteres.</td><td>false</td></tr><tr><td>impuestos_internos_alicuota</td><td>Valor numérico con hasta 2 decimales. Separador de decimales: punto</td><td>false</td></tr><tr><td>unidad_medida</td><td>Valor según tabla de referencia: "<a href="../parametros/consulta-de-unidades-de-medida-para-productos-afip.md">Unidades de medida"</a></td><td>false</td></tr><tr><td>afecta_stock</td><td>Valores posibles: "S" o "N" </td><td>true</td></tr><tr><td>stock_actual</td><td>Valor numérico entero. Éste campo se utiliza solo en el alta de productos</td><td>false</td></tr><tr><td>stock_minimo</td><td> Valor numérico entero.</td><td>false</td></tr></tbody></table>

### ¿Qué te retorna en cada llamada?

Se devolverá una lista, en el mismo orden en que se recibió, conteniendo la siguiente estructura:

```
    {
	"error": "N",
	"errores": [],
	"productos": [
		{
			"codigo": "tren10384",
			"lista_precios": "Trenes",
			"error": "N",
			"errores": []
		},
		{
			"codigo": "Cam01",
			"lista_precios": "Camiones",
			"error": "S",
			"errores": [
				"Ya existe un producto en esa lista de precios con el codigo: Cam01. No se agregara."
			]
		}
	]
}
```
