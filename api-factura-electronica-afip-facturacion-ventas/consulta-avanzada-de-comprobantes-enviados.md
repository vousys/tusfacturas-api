---
description: >-
  Mediante ésta consulta, podrás obtener todos los comprobantes enviados, según
  determinadas condiciones de búsqueda.
---

# Consulta avanzada de comprobantes enviados

### Métodos de búsqueda disponibles:

1. &#x20;Todos los comprobantes de una [determinada fecha](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-fecha)[ ](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-fecha):arrow\_right:
2. &#x20;Todos los comprobantes de un mismo tipo (Ej: FACTURA A ) entre un determinado [rango numérico](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-rango-de-numeros) (Ej: 00000010 al 00000050). [ ](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-rango-de-numeros):arrow\_right:
3. Todos los comprobantes de una misma [external reference](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-external-reference) :arrow\_right: &#x20;

{% hint style="info" %}
A partir del 01/04/2022 ésta consulta te devolverá también, todos aquellos comprobantes que se encuentren en cola de procesamiento ( pendientes de procesamiento, o  procesados por error).
{% endhint %}

#### Cómo llamar a la API?

{% swagger baseUrl="https://www.tusfacturas.app/app/api/v2" path="/facturacion/consulta_avanzada" method="post" summary="Consulta de comprobantes avanzada" %}
{% swagger-description %}
Estructura general para todo tipo de consulta avanzada
{% endswagger-description %}

{% swagger-parameter in="body" name="busqueda_tipo" type="string" required="false" %}
Campo alfanumérico.&#x20;

Valores permitidos: "F", EXT\_REF", "TN"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limite" type="int" %}
Valor entero númerico.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pagina" type="int" %}
Valor entero númerico.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" type="object" required="false" %}
Objeto atributos, según estructura que se detalla a continuación para cada tipo de búsqueda.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="Devuelve un array con cada " %}
```
```
{% endswagger-response %}
{% endswagger %}

#### Ejemplo del JSON de respuesta:

La consulta te devolverá un array, compuesto por cada comprobante, que tendrá la misma estructura que te entrega la consulta de[ comprobante simple.](api-factura-electronica-afip-consulta-de-comprobantes.md)&#x20;

Ej:

```json
{
   "rta":"OK",
   "error":"N",
   "total":3,
   "errores":[
      
   ],
   "comprobantes":[
      {
         "cliente":{
            "documento_tipo":"DNI",
            "documento_nro":"1292963535 ",
            "razon_social":"Pirulo",
            "email":"test@test.com",
            "domicilio":"Av Sta Fe 123"
         },
         "comprobante":{
            "fecha":"06\/01\/2023",
            "tipo":"FACTURA A",
            "operacion":"V",
            "punto_venta":10,
            "numero":603,
            "moneda":"PES",
            "cotizacion":1,
            "periodo_facturado_desde":"06\/01\/2023",
            "periodo_facturado_hasta":"06\/01\/2023",
            "rubro":"Deudores Varios",
            "rubro_grupo_contable":"Ventas",
            "detalle":[
               {
                  "cantidad":1,
                  "producto":{
                     "descripcion":"PRODUCTO DE PRUEBA",
                     "precio_unitario":20000,
                     "alicuota":21,
                     "bonificacion":10000,
                     "impuestos_internos_alicuota":10,
                     "precio_total":10000
                  },
                  "bonificacion_porcentaje":50,
                  "leyenda":"Hola manoala"
               }
            ],
            "bonificacion":0,
            "leyenda_gral":" ",
            "percepciones_iibb":0,
            "percepciones_iva":0,
            "tributos":[
               
            ],
            "exentos":0,
            "nogravados":0,
            "impuestos_internos":500,
            "impuestos_internos_base":5000,
            "impuestos_internos_alicuota":10,
            "total":12600,
            "cae":"73016074427512 ",
            "afip_codigo_barras":"12121212121006000300000000000000201811052 ",
            "afip_qr":"https:\/\/www.afip.gob.ar\/fe\/qr\/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjadadasdasdaAyMS0wNi0wNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjEwIiwidGlwb0NtcCI6MSwibnJvQ21wIjoiMDAwMDAwNzgiLCJpbXBvcnRlIjoiMDAwMDAwMDAwMzA4NS41MCIsIm1vbmVkYSI6IlBFUyIs ",
            "vencimiento_cae":"07\/08\/2015",
            "vencimiento_pago":"27\/08\/2015",
            "comprobante_pdf_url":"https://www.dominio.com/00000006.pdf",
            "external_reference":3303,
            "tags":[
               "etiqueta1",
               "etiqueta2"
            ],
            "status":"EMITIDO",
            "ctacte_status":"PAGO PARCIAL",
            "micrositios":{
               "cliente":"https:\/\/servicios.tusfacturas.app\/micrositios\/c\/asdsadsd\/adasdasd\/14228423\/acceder",
               "descarga":"https:\/\/servicios.tusfacturas.app\/micrositios\/descargas\/asdasd\/asdsad\/kZ8Hl9fpUb4xFDK16O\/00000602"
            }
         }
      },
      {
         "cliente":{
            "documento_tipo":"DNI",
            "documento_nro":"1292963535 ",
            "razon_social":"Pirulo",
            "email":"test@test.com",
            "domicilio":"Av Sta Fe 123"
         },
         "comprobante":{
            "fecha":"06\/12\/2022",
            "tipo":"FACTURA A",
            "operacion":"V",
            "punto_venta":10,
            "numero":602,
            "moneda":"PES",
            "cotizacion":1,
            "periodo_facturado_desde":"06\/12\/2022",
            "periodo_facturado_hasta":"06\/12\/2022",
            "rubro":"Deudores Varios",
            "rubro_grupo_contable":"Ventas",
            "detalle":[
               {
                  "cantidad":1,
                  "producto":{
                     "descripcion":"PRODUCTO DE PRUEBA",
                     "precio_unitario":20000,
                     "alicuota":21,
                     "bonificacion":10000,
                     "impuestos_internos_alicuota":10,
                     "precio_total":10000
                  },
                  "bonificacion_porcentaje":50,
                  "leyenda":"Hola manoala"
               }
            ],
            "bonificacion":0,
            "leyenda_gral":" ",
            "percepciones_iibb":0,
            "percepciones_iva":0,
            "tributos":[
               
            ],
            "exentos":0,
            "nogravados":0,
            "impuestos_internos":1000,
            "impuestos_internos_base":10000,
            "impuestos_internos_alicuota":10,
            "total":13100,
            "cae":"72496063743552 ",
            "afip_codigo_barras":"12121212121006000300000000000000201811052 ",
            "afip_qr":"https:\/\/www.afip.gob.ar\/fe\/qr\/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjadadasdasdaAyMS0wNi0wNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjEwIiwidGlwb0NtcCI6MSwibnJvQ21wIjoiMDAwMDAwNzgiLCJpbXBvcnRlIjoiMDAwMDAwMDAwMzA4NS41MCIsIm1vbmVkYSI6IlBFUyIs ",
            "vencimiento_cae":"07\/08\/2015",
            "vencimiento_pago":"27\/08\/2015",
            "comprobante_pdf_url":"https://www.dominio.com/00000006.pdf",
            "external_reference":"",
            "tags":[
               
            ],
            "status":"EMITIDO",
            "ctacte_status":"IMPAGA",
            "micrositios":{
               "cliente":"https:\/\/servicios.tusfacturas.app\/micrositios\/c\/asdsadsd\/adasdasd\/14228423\/acceder",
               "descarga":"https:\/\/servicios.tusfacturas.app\/micrositios\/descargas\/asdasd\/asdsad\/kZ8Hl9fpUb4xFDK16O\/00000602"
            }
         }
      },
      {
         "cliente":{
            "documento_tipo":"DNI",
            "documento_nro":"1292963535 ",
            "razon_social":"Pirulo",
            "email":"test@test.com",
            "domicilio":"Av Sta Fe 123"
         },
         "comprobante":{
            "fecha":"02\/11\/2022",
            "tipo":"FACTURA A",
            "operacion":"V",
            "punto_venta":10,
            "numero":601,
            "moneda":"PES",
            "cotizacion":1,
            "periodo_facturado_desde":"02\/11\/2022",
            "periodo_facturado_hasta":"02\/11\/2022",
            "rubro":"Deudores varios",
            "rubro_grupo_contable":"Deudores varios",
            "detalle":[
               {
                  "cantidad":1,
                  "producto":{
                     "descripcion":"Gomas de borrar",
                     "precio_unitario":200,
                     "alicuota":0,
                     "bonificacion":0,
                     "impuestos_internos_alicuota":0,
                     "precio_total":200
                  },
                  "bonificacion_porcentaje":0,
                  "leyenda":""
               }
            ],
            "bonificacion":0,
            "leyenda_gral":" ",
            "percepciones_iibb":0,
            "percepciones_iva":0,
            "tributos":[
               
            ],
            "exentos":0,
            "nogravados":0,
            "impuestos_internos":0,
            "impuestos_internos_base":0,
            "impuestos_internos_alicuota":0,
            "total":200,
            "cae":"72446045034650 ",
            "afip_codigo_barras":"12121212121006000300000000000000201811052 ",
            "afip_qr":"https:\/\/www.afip.gob.ar\/fe\/qr\/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjadadasdasdaAyMS0wNi0wNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjEwIiwidGlwb0NtcCI6MSwibnJvQ21wIjoiMDAwMDAwNzgiLCJpbXBvcnRlIjoiMDAwMDAwMDAwMzA4NS41MCIsIm1vbmVkYSI6IlBFUyIs ",
            "vencimiento_cae":"07\/08\/2015",
            "vencimiento_pago":"27\/08\/2015",
            "comprobante_pdf_url":"https://www.dominio.com/00000006.pdf",
            "external_reference":"",
            "tags":[
               
            ],
            "status":"EMITIDO",
            "ctacte_status":"IMPAGA",
            "micrositios":{
               "cliente":"https:\/\/servicios.tusfacturas.app\/micrositios\/c\/asdsadsd\/adasdasd\/14228423\/acceder",
               "descarga":"https:\/\/servicios.tusfacturas.app\/micrositios\/descargas\/asdasd\/asdsad\/kZ8Hl9fpUb4xFDK16O\/00000602"
            }
         }
      }
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

## ¿Cómo realizar una consulta avanzada por fecha?

La búsqueda por fecha te devuelve todos aquellos comprobantes enviados (ya sea porque se han emitido o porque se encuentren en la cola de facturación) en la fecha consultada.&#x20;

Debés tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

{% hint style="info" %}
A partir del 01/05/2022, está consultá comenzará a ser paginada, con un límite máximo de registros por página de 1,000.&#x20;
{% endhint %}

#### Ejemplo de JSON a enviar para consultar por fecha un comprobante:

Tipo de datos: **JSON**\
Charset: **UTF-8**

```json
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",json
"busqueda_tipo": "F",
 "pagina" : 0,
 "limite": 100 ,
"comprobante":  {
                "fecha":     "23/05/2021",
                "operacion": "V"
        }
}
```

#### Detalle de los atributos a enviar:

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



#### Que te devolverá ?

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

## ¿Cómo realizar una consulta avanzada, por rango de números?

Ésta búsqueda te permite obtener todos los comprobantes enviados, ya sea porque se han emitido o porque se encuentren en la cola de facturación, dentro de un rango numérico.&#x20;

Debés tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

{% hint style="info" %}
A partir del 01/05/2022, está consultá comenzará a ser paginada, con un límite máximo de registros por página de 1,000.&#x20;
{% endhint %}

#### Detalle de los atributos a enviar:

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

#### Ejemplo del JSON a enviar :

```json
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"busqueda_tipo": "TN",
 "pagina" : 0,
 "limite": 100 ,
"comprobante": 
	{
			"tipo": "FACTURA A",
			"operacion": "V",
			"punto_venta": "00010",
			"numero_desde": "00000001",
			"numero_hasta": "00000300" 
			 
	}
} 
```

#### Que te devolverá ?

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



## ¿Cómo realizar una consulta avanzada, por external reference?

{% hint style="info" %}
Ésta consulta estará disponible a partir del 01/04/2022&#x20;
{% endhint %}

Ésta búsqueda te permite obtener todos los comprobantes enviados, ya sea porque se han emitido o porque se encuentren en la cola de facturación, de una determinada external\_reference.&#x20;

Debés tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

#### Detalle de los atributos a enviar:

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



#### Ejemplo del JSON a enviar :

```json
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"busqueda_tipo": "EXT_REF",
 "pagina" : 0,
 "limite": 100 ,
"comprobante": {
		"external_reference": "DD2F1F1",
		"operacion": "V"
	}
} 
```

#### Que te devolverá ?

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

