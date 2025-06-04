---
description: >-
  Mediante ésta consulta podrás obtener todos los comprobantes enviados, según
  determinadas condiciones de búsqueda.
---

# Consulta avanzada

La **API ARCA/AFIP de TusFacturasAPP** ofrece dos métodos para consultar comprobantes fiscales emitidos desde tu sistema: el método de [**consulta simple**](api-factura-electronica-afip-consulta-de-comprobantes.md) y el de **consulta avanzada**. Ambos son fundamentales para verificar el estado y obtener los datos de las ventas realizadas.

### 🔹 Consulta avanzada de ventas

Nuestra herramienta de Consulta Avanzada de Ventas está diseñada para ir más allá de una búsqueda simple, permitiéndote **explorar y recuperar información específica** de tus operaciones  de manera profunda.

Podrás aplicar diferentes **filtros** para refinar tus resultados, lo cual te permite obtener **reportes precisos y segmentados**, facilitando un análisis exhaustivo de tus ventas. &#x20;



⚠️ **Consideraciones importantes:**

* La información obtenida se limita a los comprobantes del punto de venta desde el cual se realiza la solicitud.
* Los resultados se ordenan de forma descendente por fecha de emisión y orden de llegada (del más reciente al más antiguo).
* La consulta te devolverá los resultados paginados, con un límite máximo de ventas por página es de 1.000
* El uso de éste método **no contabiliza como un request** en tu suscripción

### 🛠️ Estructura del request a enviar:

| Name           | Type   | Description                                                                                  |
| -------------- | ------ | -------------------------------------------------------------------------------------------- |
| busqueda\_tipo | string | <p>Campo alfanumérico. </p><p>Valores permitidos: "F", "EXT_REF", "TN"</p>                   |
| comprobante    | object | Objeto atributos, según estructura que se detalla a continuación para cada tipo de búsqueda. |
| usertoken      | string | Tus credenciales de acceso                                                                   |
| apitoken       | string | Tus credenciales de acceso                                                                   |
| apikey         | string | Tus credenciales de acceso                                                                   |
| limite         | int    | Valor entero númerico.                                                                       |
| pagina         | int    | Valor entero númerico.                                                                       |

### Ejemplo del JSON de respuesta:

La respuesta contendrá un array de comprobantes (emitidos o pendientes de emisión). **Cada comprobante en este array sigue la misma estructura que la** [**consulta simple**](api-factura-electronica-afip-consulta-de-comprobantes.md#ejemplo-del-json-de-respuesta)**.**

```json
{
   "rta":"OK",
   "error":"N",
   "total":3,
   "errores":[
      
   ],
   "comprobantes":[
      {comprobante_ver_json_respuesta_consulta_simple} ,
      {comprobante_ver_json_respuesta_consulta_simple} ,
      {comprobante_ver_json_respuesta_consulta_simple}   
      ]
}
```

#### Detalle de los campos de la respuesta

| Nombre del campo | Info                                                                                                                                                                               |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| error            | Campo alfanumerico. Valores posibles "S" o "N"                                                                                                                                     |
| errores          | Array conteniendo la lista de errores detectados                                                                                                                                   |
| total            | Campo numérico, que indica la cantidad de registros encontrados con los parámetros indicados, sin aplicarle la paginación ni limitación. (Dato disponible a partir del 01/04/2022) |
| comprobantes     | Array conteniendo cada uno de los comprobantes encontrados, según estructura que se detalla en la [consulta simple.](api-factura-electronica-afip-consulta-de-comprobantes.md)     |
|                  |                                                                                                                                                                                    |

A continuación te mostramos las diferentes opciones de búsqueda avanzada de ventas:&#x20;

### 📅 Consulta por Fecha de Emisión&#x20;

Esta consulta retorna todos los comprobantes cuya fecha de emisión coincide exactamente con la fecha solicitada.

#### :rocket: Ejemplo del JSON a enviar:

{% content-ref url="../web-services-afip-api-arca/consulta-avanzada-por-fecha.md" %}
[consulta-avanzada-por-fecha.md](../web-services-afip-api-arca/consulta-avanzada-por-fecha.md)
{% endcontent-ref %}

#### ¿Cómo armar el bloque "comprobante" para usar ésta búsqueda?

| `operacion` | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p> |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `fecha`     | <p>Campo fecha en formato dd/mm/aaaa<br><strong>Ejemplo: 20/03/2022</strong></p>                                                                                                      |

#### Ejemplo del JSON de respuesta:

La respuesta contendrá un array de comprobantes (emitidos o pendientes de emisión). **Cada comprobante en este array sigue la misma estructura que la** [**consulta simple**](api-factura-electronica-afip-consulta-de-comprobantes.md#ejemplo-del-json-de-respuesta)**.**

```json
{
	"rta": "OK",
	"error": "N",
	"total": 4,
	"errores": [],
	"comprobantes": [
		{comprobante_ver_json_respuesta_consulta_simple},
		{comprobante_ver_json_respuesta_consulta_simple},
		{comprobante_ver_json_respuesta_consulta_simple},
		{comprobante_ver_json_respuesta_consulta_simple}
		]
}

```

***

### 🔍 Consulta avanzada por rango de números

Este método te permite recuperar todos los comprobantes asociados a un punto de venta dentro de un rango numérico determinado. Podrás obtener tanto comprobantes **ya emitidos** como aquellos que aún se encuentran **en cola de procesamiento**.

#### :rocket: Ejemplo del JSON a enviar:

{% content-ref url="../web-services-afip-api-arca/consulta-avanzada-por-numero.md" %}
[consulta-avanzada-por-numero.md](../web-services-afip-api-arca/consulta-avanzada-por-numero.md)
{% endcontent-ref %}

#### ¿Cómo armar el bloque "comprobante" para usar ésta búsqueda?

| `tipo`         | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`    | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta`  | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero_desde` | <p>Campo numérico entero. Longitud máxima 8 dígitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |
| `numero_hasta` | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |

#### Ejemplo del JSON de respuesta:

La respuesta contendrá un array de comprobantes (emitidos o pendientes de emisión). **Cada comprobante en este array sigue la misma estructura que la** [**consulta simple**](api-factura-electronica-afip-consulta-de-comprobantes.md#ejemplo-del-json-de-respuesta)

```json
{
	"rta": "OK",
	"error": "N",
	"total": 4,
	"errores": [],
	"comprobantes": [
		{comprobante_ver_consulta_simple},
		{comprobante_ver_consulta_simple},
		{comprobante_ver_consulta_simple},
		{comprobante_ver_consulta_simple}
		]
}
```



***

### 🔎 Consulta avanzada por `external_reference`

Esta consulta permite obtener todos los comprobantes relacionados a un valor específico de `external_reference`, ya sea que estén **emitidos** o **en cola de facturación**.&#x20;

#### Ejemplo del JSON a enviar:

{% content-ref url="../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md" %}
[consulta-avanzada-por-external-reference.md](../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md)
{% endcontent-ref %}

#### ¿Cómo armar el bloque "comprobante" para usar ésta búsqueda?

| `external_reference` | Campo alfanumérico. Longitud mínima: 1 carácter                                                                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`          | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p> |

#### Ejemplo del JSON de respuesta:

La respuesta contendrá un array de comprobantes (emitidos o pendientes de emisión). **Cada comprobante en este array sigue la misma estructura que la** [**consulta simple**](api-factura-electronica-afip-consulta-de-comprobantes.md#ejemplo-del-json-de-respuesta)

```json
{
	"rta": "OK",
	"error": "N",
	"total": 4,
	"errores": [],
	"comprobantes": [
		{comprobante_ver_consulta_simple},
		{comprobante_ver_consulta_simple},
		{comprobante_ver_consulta_simple},
		{comprobante_ver_consulta_simple}
		]
}
```

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
