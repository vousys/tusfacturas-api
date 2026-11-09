---
description: >-
  Mediante ésta consulta podrás obtener todos los comprobantes enviados, según
  determinadas condiciones de búsqueda.
icon: magnifying-glass
---

# Consulta avanzada: listar comprobantes por fecha, rango o external reference

Devuelve una lista paginada de comprobantes, emitidos o en cola, que cumplen un criterio de búsqueda. Para un comprobante puntual del que sabés tipo, punto de venta y número, usá la [consulta simple](api-factura-electronica-afip-consulta-de-comprobantes.md).

#### Endpoint

{% hint style="success" icon="rectangle-api" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`consulta_avanzada`</mark>
{% endhint %}

{% hint style="info" %}
&#x20;🪙 **Consumo de créditos:** este método no consume créditos.&#x20;
{% endhint %}

#### Cómo funciona

* Devuelve solo los comprobantes del punto de venta desde el cual se hace la consulta.
* Ordena los resultados del más reciente al más antiguo, por fecha de emisión y orden de llegada.
* Pagina los resultados: hasta 1.000 comprobantes por página.

#### Tipos de búsqueda

| Buscar por                | `busqueda_tipo` | Campos del bloque `comprobante`                                    | Ejemplos de código                                                               |
| ------------------------- | --------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| Fecha de emisión          | `F`             | `operacion`, `fecha`                                               | [Ver](../web-services-afip-api-arca/consulta-avanzada-por-fecha.md)              |
| Rango de números          | `TN`            | `operacion`, `tipo`, `punto_venta`, `numero_desde`, `numero_hasta` | [Ver](../web-services-afip-api-arca/consulta-avanzada-por-numero.md)             |
| Un external reference     | `EXT_REF`       | `operacion`, `external_reference`                                  | [Ver](../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md) |
| Varios external reference | `EXT_REF_LIST`  | `operacion`, `external_reference_list`                             | [Ver](../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md) |

#### Estructura del request

Campos comunes a todos los tipos de búsqueda:

| Campo           | Tipo     | Requerido | Descripción                                                  |
| --------------- | -------- | --------- | ------------------------------------------------------------ |
| `apikey`        | string   | Sí        | Credencial de acceso. [Cómo obtenerla](../como-empiezo/)     |
| `apitoken`      | string   | Sí        | Credencial de acceso                                         |
| `usertoken`     | string   | Sí        | Credencial de acceso                                         |
| `busqueda_tipo` | string   | Sí        | `F`, `TN`, `EXT_REF` o `EXT_REF_LIST`. Ver tabla anterior    |
| `pagina`        | numérico | Sí        | Número de página. La primera es `0`                          |
| `limite`        | numérico | Sí        | Cantidad de comprobantes por página, hasta `1000`            |
| `comprobante`   | objeto   | Sí        | Criterio de búsqueda. Sus campos dependen de `busqueda_tipo` |

Para obtener todos los resultados, pedí `pagina` 0, 1, 2… hasta que una página traiga menos comprobantes que `limite`. El campo `total` de la respuesta indica cuántos hay en total.

***

#### Consulta por fecha de emisión

Devuelve los comprobantes cuya fecha de emisión coincide exactamente con la fecha indicada.

| Campo       | Tipo   | Descripción                               |
| ----------- | ------ | ----------------------------------------- |
| `operacion` | string | `V` para ventas, `C` para compras         |
| `fecha`     | string | Formato dd/mm/aaaa. Ejemplo: `23/05/2021` |

```json
{
  "usertoken": "xxxx",
  "apikey": "xxxx",
  "apitoken": "xxxx",
  "busqueda_tipo": "F",
  "pagina": 0,
  "limite": 100,
  "comprobante": {
    "fecha": "23/05/2021",
    "operacion": "V"
  }
}
```

***

#### Consulta avanzada por rango de números

Devuelve los comprobantes de un tipo y punto de venta dentro de un rango de números, tanto los emitidos como los que siguen en cola de procesamiento.

| Campo          | Tipo     | Descripción                                                                                                      |
| -------------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| `operacion`    | string   | `V` para ventas, `C` para compras                                                                                |
| `tipo`         | string   | Tipo de comprobante, según la [tabla de referencia](../parametros/tablas-de-referencia.md). Ejemplo: `FACTURA A` |
| `punto_venta`  | numérico | Hasta 4 dígitos                                                                                                  |
| `numero_desde` | numérico | Primer número del rango, hasta 8 dígitos                                                                         |
| `numero_hasta` | numérico | Último número del rango, hasta 8 dígitos                                                                         |

```json
{
  "usertoken": "xxxx",
  "apikey": "xxxx",
  "apitoken": "xxxx",
  "busqueda_tipo": "TN",
  "pagina": 0,
  "limite": 100,
  "comprobante": {
    "tipo": "FACTURA A",
    "operacion": "V",
    "punto_venta": "00010",
    "numero_desde": "00000001",
    "numero_hasta": "00000300"
  }
}
```

***

#### Consulta avanzada por external\_reference

Devuelve los comprobantes, emitidos o en cola, asociados al identificador que tu sistema envió en `external_reference` al emitirlos. Podés buscar un valor o varios a la vez.

**Un solo external reference**

| Campo                | Tipo   | Descripción                       |
| -------------------- | ------ | --------------------------------- |
| `operacion`          | string | `V` para ventas, `C` para compras |
| `external_reference` | string | Valor a buscar. Mínimo 1 carácter |

```json
{
  "usertoken": "xxxx",
  "apikey": "xxxx",
  "apitoken": "xxxx",
  "busqueda_tipo": "EXT_REF",
  "pagina": 0,
  "limite": 100,
  "comprobante": {
    "external_reference": "ABC1234",
    "operacion": "V"
  }
}
```

**Varios external reference (BULK)**

| Campo                     | Tipo             | Descripción                                          |
| ------------------------- | ---------------- | ---------------------------------------------------- |
| `operacion`               | string           | `V` para ventas, `C` para compras                    |
| `external_reference_list` | array de strings | Hasta 100 valores. Ejemplo: `["ABC1234", "ABC1235"]` |

{% hint style="warning" %}
Un pedido muy grande puede ser bloqueado por el firewall. Si te pasa, enviá menos valores por pedido.&#x20;
{% endhint %}

```json
{
  "usertoken": "xxxx",
  "apikey": "xxxx",
  "apitoken": "xxxx",
  "busqueda_tipo": "EXT_REF_LIST",
  "pagina": 0,
  "limite": 100,
  "comprobante": {
    "external_reference_list": ["ABC1234", "ABC1235", "ABC188"],
    "operacion": "V"
  }
}
```

***

#### Respuesta

La respuesta es la misma para todos los tipos de búsqueda: un encabezado con el resultado y la lista `comprobantes`.

{% hint style="info" %}
Cada elemento de `comprobantes` tiene **la misma estructura que la respuesta de la** [**consulta simple**](api-factura-electronica-afip-consulta-de-comprobantes.md). Ahí está el JSON completo y la descripción de cada campo.&#x20;
{% endhint %}

Estructura de la respuesta:

```javascript
{
  "rta": "OK",
  "error": "N",
  "errores": [],
  "total": 3,
  "comprobantes": [
    { /* comprobante 1: misma estructura que la respuesta de la consulta simple */ },
    { /* comprobante 2 */ },
    { /* comprobante 3 */ }
  ]
}
```



| Campo          | Descripción                                                                                                              |
| -------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `error`        | `N` si la consulta funcionó, `S` si hubo errores                                                                         |
| `errores`      | Lista de errores. Vacía si `error` es `N`                                                                                |
| `total`        | Cantidad total de comprobantes que cumplen el criterio, sin aplicar paginación ni límite. Disponible desde el 01/04/2022 |
| `comprobantes` | Lista con los comprobantes de la página pedida                                                                           |

#### ¿Aún te quedan dudas? ¡Contactanos!

Si necesitas asistencia con tu plan API DEV, escribinos a [api@tusfacturas.app](mailto:api@tusfacturas.app) o por el [chat de nuestra web](https://www.tusfacturas.app/contacto.html).

