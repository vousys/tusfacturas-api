---
description: >-
  Gestiona tus productos con facilidad y eficiencia con nuestra API de
  productos.
---

# Consultar productos

## Consultá productos

Éste método te permite enviar un lote de hasta 50 productos para consultar.

{% hint style="info" %}
### ¿Qué debes tener en cuenta?



* El código de producto debe ser único dentro de la lista de precios
* Podes enviar hasta 50 productos por request.


{% endhint %}

### Request

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/productos/consultar`

#### Request Body

| Name      | Type   | Description                                                                                                                            |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| productos | array  | **Una lista de objetos "**[**producto**](api-factura-electronica-afip-clientes-cuenta-corriente-1.md#estructura-de-cada-producto)**"** |
| usertoken | string | Tus credenciales de acceso                                                                                                             |
| apikey    | string | Tus credenciales de acceso                                                                                                             |
| apitoken  | string | Tus credenciales de acceso                                                                                                             |

### Ejemplo del JSON que debes enviar

```
{
    "usertoken": "xxxx",
    "apikey": "xxxx",
    "apitoken": "xxxx",
    "productos": [
        {
            "lista_precios": "Trenes",
            "codigo": "tren10384"
        },
        {
            "lista_precios": "Camiones",
            "codigo": "Cam01"
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
            "error": "N",
            "errores": [],
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
            "error": "N",
            "errores": [],
            "descripcion": "Camion de arena",
            "unidad_bulto": "1",
            "lista_precios": "Camiones",
            "codigo": "Cam01",
            "precio_unitario_sin_iva": 1000,
            "alicuota": 21,
            "moneda": "PES",
            "codbar": "",
            "impuestos_internos_alicuota": 0,
            "unidad_medida": "7",
            "afecta_stock": "S",
            "stock_actual": 154,
            "stock_minimo": 500
        }
    ]
}

```
