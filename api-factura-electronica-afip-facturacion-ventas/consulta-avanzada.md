---
description: >-
  Mediante ésta consulta podrás obtener todos los comprobantes enviados, según
  determinadas condiciones de búsqueda.
---

# Consulta avanzada

💡 El uso de éste método no contabiliza como un request en tu suscripción

### Parámetros

| Name           | Type   | Description                                                                                  |
| -------------- | ------ | -------------------------------------------------------------------------------------------- |
| busqueda\_tipo | string | <p>Campo alfanumérico. </p><p>Valores permitidos: "F", "EXT_REF", "TN"</p>                   |
| comprobante    | object | Objeto atributos, según estructura que se detalla a continuación para cada tipo de búsqueda. |
| usertoken      | string | Tus credenciales de acceso                                                                   |
| apitoken       | string | Tus credenciales de acceso                                                                   |
| apikey         | string | Tus credenciales de acceso                                                                   |
| limite         | int    | Valor entero númerico.                                                                       |
| pagina         | int    | Valor entero númerico.                                                                       |

#### Ejemplo del JSON de respuesta:

La consulta te devolverá un array con cada comprobante encontrado (emitido o pendiente de emisión), que tendrá la misma estructura que te entrega la consulta de[ comprobante simple.](api-factura-electronica-afip-consulta-de-comprobantes.md)&#x20;

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

#### Campos de la respuesta

| Nombre del campo | Info                                                                                                                                                                               |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| error            | Campo alfanumerico. Valores posibles "S" o "N"                                                                                                                                     |
| errores          | Array conteniendo la lista de errores detectados                                                                                                                                   |
| total            | Campo numérico, que indica la cantidad de registros encontrados con los parámetros indicados, sin aplicarle la paginación ni limitación. (Dato disponible a partir del 01/04/2022) |
| comprobantes     | Array conteniendo cada uno de los comproantes encontrados, según estructura que se detalla en la [consulta simple.](api-factura-electronica-afip-consulta-de-comprobantes.md)      |

## :date:  Consulta de ventas en una determinada fecha

La búsqueda por fecha te devuelve todos aquellos comprobantes enviados para la fecha consultada. Debes tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

{% hint style="info" %}
A partir del 01/05/2022, está consultá comenzará a ser paginada, con un límite máximo de registros por página de 1,000.&#x20;
{% endhint %}

#### :rocket: ¿Cómo enviar una consulta para obtener las ventas en una determinada fecha?

Ejemplo:

{% content-ref url="../web-services-afip-api-arca/consulta-avanzada-por-fecha.md" %}
[consulta-avanzada-por-fecha.md](../web-services-afip-api-arca/consulta-avanzada-por-fecha.md)
{% endcontent-ref %}

#### Parámetros:

|    Atributo    |                    Valores esperados                   |
| :------------: | :----------------------------------------------------: |
| busqueda\_tipo |          Campo alfanumérico esperado: "**F**"          |
|   comprobante  |         Objeto según se detalla a continuación         |
|     pagina     |        Valor numérico entero. Mínimo esperado: 0       |
|     limite     | Valor numérico entero. Mínimo esperado: 0 Máximo: 1000 |

#### Estructura de "Comprobante":

| `operacion` | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p> |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `fecha`     | <p>Campo fecha en formato dd/mm/aaaa<br><strong>Ejemplo: 20/03/2022</strong></p>                                                                                                      |

¿Qué te devolverá ?

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



### :1234: Consulta avanzada  por rango de números

Ésta búsqueda te permite obtener todos los comprobantes enviados, ya sea porque se han emitido o porque se encuentren en la cola de facturación, dentro de un rango numérico. Debés tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

{% hint style="info" %}
A partir del 01/05/2022, está consultá comenzará a ser paginada, con un límite máximo de registros por página de 1,000.&#x20;
{% endhint %}

#### :rocket: ¿Cómo enviar una consulta para obtener las ventas por un rango numérico?

Ejemplo:

{% content-ref url="../web-services-afip-api-arca/consulta-avanzada-por-numero.md" %}
[consulta-avanzada-por-numero.md](../web-services-afip-api-arca/consulta-avanzada-por-numero.md)
{% endcontent-ref %}



#### Parámetros:

|    Atributo    |                    Valores esperados                   |
| :------------: | :----------------------------------------------------: |
| busqueda\_tipo |          Campo alfanumérico esperado: "**TN**"         |
|   comprobante  |         Objeto según se detalla a continuación         |
|     pagina     |        Valor numérico entero. Mínimo esperado: 0       |
|     limite     | Valor numérico entero. Mínimo esperado: 0 Máximo: 1000 |

#### Estructura de "Comprobante":

| `tipo`         | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`    | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta`  | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero_desde` | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |
| `numero_hasta` | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |

#### ¿Qué te devolverá ?

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



### :abc:  Consulta avanzada  por external reference

Ésta búsqueda te permite obtener todos los comprobantes enviados, ya sea porque se han emitido o porque se encuentren en la cola de facturación, **de una determinada external\_reference.** Debes tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

#### Parámetros:

|    Atributo    |                    Valores esperados                   |
| :------------: | :----------------------------------------------------: |
| busqueda\_tipo |    Campo alfanumérico, valor esperado: "**EXT\_REF**   |
|   comprobante  |         Objeto según se detalla a continuación         |
|     pagina     |        Valor númerico entero. Mínimo esperado: 0       |
|     limite     | Valor númerico entero. Mínimo esperado: 0 Máximo: 1000 |

#### Estructura de "Comprobante":

| `external_reference` | Campo alfanumérico. Longitud mínima: 1 carácter                                                                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`          | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p> |

#### :rocket: ¿Cómo enviar una consulta para obtener las ventas por external reference?

Ejemplo:

{% content-ref url="../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md" %}
[consulta-avanzada-por-external-reference.md](../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md)
{% endcontent-ref %}



#### ¿Qué te devolverá ?

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

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
