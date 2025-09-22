---
description: >-
  Gestiona tus productos con facilidad y eficiencia con nuestra API de
  productos.
---

# Listar productos

## Lista tus productos

Éste método te permite consultar todos los productos/servicios registrados y mantener un sincronismo entre tu plataforma y TusFacturasAPP.

### Request

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`productos/listar`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

| Name            | Type     | Description                                                                       |
| --------------- | -------- | --------------------------------------------------------------------------------- |
| orden\_criterio | string   | Un solo valor a enviar. Valores permitidos:  fecha\_creacion, descripcion, codigo |
| orden           | string   | Valores permitidos: ASC, DESC                                                     |
| pagina          | numérico | Inicia en 0.                                                                      |
| limite          | numerico | Numerico. Máximo: 1000                                                            |
| usertoken       | string   | Tus credenciales de acceso                                                        |
| apikey          | string   | Tus credenciales de acceso                                                        |
| apitoken        | string   | Tus credenciales de acceso                                                        |



{% hint style="info" %}
**Datos a tener en cuenta:**

* La información se obtiene paginada. La pagina inicial es 0.
* El limite máximo de registros por consulta es 1000.
* El criterio de orden solo puede ser un valor&#x20;
{% endhint %}

### Ejemplo del JSON que debes enviar

```
{
    "usertoken": "xxxx",
    "apikey": "xxxx",
    "apitoken": "xxxx",
    "orden_criterio": "fecha_creacion", 
     "orden": "DESC",
     "limite": 10,
     "pagina": 5
}
```



### ¿Qué te retorna en cada llamada?

| Nombre del campo | Info                                                                                                                                     |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| error            | Campo alfanumerico. Valores posibles "S" o "N"                                                                                           |
| errores          | Array conteniendo la lista de errores detectados                                                                                         |
| total            | Campo numérico, que indica la cantidad de registros encontrados con los parámetros indicados, sin aplicarle la paginación ni limitación. |
| productos        | Array conteniendo cada uno de los productos encontrados                                                                                  |
|                  |                                                                                                                                          |

Se devolverá una lista,  conteniendo la siguiente estructura:

```
    {
    "error": "N",
    "errores": [], 
    "total": 20133,
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
