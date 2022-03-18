---
description: >-
  Mediante ésta consulta, podrás obtener todos los comprobantes enviados, según
  determinadas condiciones de búsqueda.
---

# Consulta avanzada de comprobantes enviados

### Métodos de búsqueda disponibles:

1. &#x20;Todos los comprobantes de una determinada fecha[ ](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-fecha):arrow\_right:
2. &#x20;Todos los comprobantes de un mismo tipo (Ej: FACTURA A ) entre un determinado rango numérico (Ej: 00000010 al 00000050). [ ](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-rango-de-numeros):arrow\_right:
3. Todos los comprobantes de una misma external reference :arrow\_right: &#x20;

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

```
{
	"error": "N",
	"errores": [],
	"rta": "OK",
	"total": 10,
	"comprobantes": [ 
	{
		"cliente": {
			"documento_tipo": "DNI",
			"documento_nro": "1292963535 ",
			"razon_social": "Pirulo",
			"email": "test@test.com",
			"domicilio": "Av Sta Fe 123"
		},
		"comprobante": {
			"fecha": "23\/05\/2021",
			"tipo": "NOTA DE DEBITO B",
			"moneda": "PES",
			"idioma": 1,
			"cotizacion": 1,
			"operacion": "V",
			"punto_venta": 2,
			"numero": 6,
			"periodo_facturado_desde": "27\/07\/2015",
			"periodo_facturado_hasta": "30\/07\/2015",
			"rubro": "Servicios web",
			"rubro_grupo_contable": "servicios",
			"detalle": [{
				"cantidad": 1,
				"producto": {
					"descripcion": "PAPAS",
					"precio_unitario": 121.54,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 121.54
	 			},
				"leyenda": "blanca, cepillada"
			}, {
				"cantidad": 1.5,
				"producto": {
					"descripcion": "HUEVOS",
					"precio_unitario": 60.50,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 90.75
					
				},
				"leyenda": ""
			}, {
				"cantidad": 2,
				"producto": {
					"descripcion": "ZANAHORIA",
					"precio_unitario": 242,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 484 
	           },
				"leyenda": ""
			} ],
			"bonificacion": 120,
			"leyenda_gral": "bla bla bla",
	        	"percepciones_iibb":        "0",
	       		"percepciones_iibb_base":   "0",
	        	"percepciones_iibb_alicuota": "0",
	        	"percepciones_iva":         "0",
	        	"percepciones_iva_base":    "0",
	        	"percepciones_iva_alicuota": "0",
	     		"exentos":                  "0",
	        	"impuestos_internos":       "0",
	        	"impuestos_internos_base":   "0",
	        	"impuestos_internos_alicuota": "0" ,
			"nogravados": 0,
			"total": 543.21,
			"cae": "65301278726386 ",
			"afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
			"afip_qr": "https:\/\/www.afip.gob.ar\/fe\/qr\/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjAyMS0wNi0wNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjEwIiwidGlwb0NtcCI6MSwibnJvQ21wIjoiMDAwMDAwNzgiLCJpbXBvcnRlIjoiMDAwMDAwMDAwMzA4NS41MCIsIm1vbmVkYSI6IlBFUyIs ",
			"vencimiento_cae": "30\/05\/2021",
			"vencimiento_pago": "23\/05\/2021",
			"external_reference": "Lun141",
			"tags": [
				"etiqueta1",
				"etiqueta2"
				],
			"ctacte_status
			"status": "EMITIDO", 
			"ctacte_status": "IMPAGA",
			"comprobante_pdf_url": "https://www.dominio.com/00000006.pdf"
		}
	},

	{
		"cliente": {
			"documento_tipo": "DNI",
			"documento_nro": "1292963535 ",
			"razon_social": "Pirulo",
			"email": "test@test.com",
			"domicilio": "Av Sta Fe 123"
		},
		"comprobante": {
			"fecha": "23\/05\/2021",
			"tipo": "NOTA DE DEBITO B",
			"moneda": "PES",
			"idioma": 1,
			"cotizacion": 1,
			"operacion": "V",
			"punto_venta": 2,
			"numero": 5,
			"periodo_facturado_desde": "27\/07\/2015",
			"periodo_facturado_hasta": "30\/07\/2015",
			"rubro": "Servicios web",
			"rubro_grupo_contable": "servicios",
			"detalle": [{
				"cantidad": 1,
				"producto": {
					"descripcion": "PAPAS",
					"precio_unitario": 121.54,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 121.54
	 			},
				"leyenda": "blanca, cepillada"
			}, {
				"cantidad": 1.5,
				"producto": {
					"descripcion": "HUEVOS",
					"precio_unitario": 60.50,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 90.75
					
				},
				"leyenda": ""
			}, {
				"cantidad": 2,
				"producto": {
					"descripcion": "ZANAHORIA",
					"precio_unitario": 242,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 484 
	           },
				"leyenda": ""
			} ],
			"bonificacion": 120,
			"leyenda_gral": "bla bla bla",
	        	"percepciones_iibb":        "0",
	        	"percepciones_iibb_base":   "0",
	        	"percepciones_iibb_alicuota": "0",
	        	"percepciones_iva":         "0",
	        	"percepciones_iva_base":    "0",
	        	"percepciones_iva_alicuota": "0",
	     		"exentos":                  "0",
	        	"impuestos_internos":       "0",
	        	"impuestos_internos_base":   "0",
	        	"impuestos_internos_alicuota": "0" ,
			"nogravados": 0,
			"total": 543.21,
			"cae": " ",
			"afip_codigo_barras" : " ",
			"afip_qr": "",
			"vencimiento_cae": "",
			"vencimiento_pago": "23\/05\/2021",
			"external_reference": "Lun141",
			"tags": [
				"etiqueta1",
				"etiqueta2"
				],
			"status": "ENVIADO A PROCESAR - CON ERROR",
			"ctacte_status": "",
			"comprobante_pdf_url": ""
		}
	},
	
		{
		"cliente": {
			"documento_tipo": "DNI",
			"documento_nro": "1292963535 ",
			"razon_social": "Pirulo",
			"email": "test@test.com",
			"domicilio": "Av Sta Fe 123"
		},
		"comprobante": {
			"fecha": "23\/05\/2021",
			"tipo": "NOTA DE DEBITO B",
			"moneda": "PES",
			"idioma": 1,
			"cotizacion": 1,
			"operacion": "V",
			"punto_venta": 2,
			"numero": 5,
			"periodo_facturado_desde": "27\/07\/2015",
			"periodo_facturado_hasta": "30\/07\/2015",
			"rubro": "Servicios web",
			"rubro_grupo_contable": "servicios",
			"detalle": [{
				"cantidad": 1,
				"producto": {
					"descripcion": "PAPAS",
					"precio_unitario": 121.54,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 121.54
	 			},
				"leyenda": "blanca, cepillada"
			}, {
				"cantidad": 1.5,
				"producto": {
					"descripcion": "HUEVOS",
					"precio_unitario": 60.50,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 90.75
					
				},
				"leyenda": ""
			}, {
				"cantidad": 2,
				"producto": {
					"descripcion": "ZANAHORIA",
					"precio_unitario": 242,
					"alicuota": 21,
					"unidad_medida": 7,
					"precio_total": 484 
	           },
				"leyenda": ""
			} ],
			"bonificacion": 120,
			"leyenda_gral": "bla bla bla",
	        	"percepciones_iibb":        "0",
	        	"percepciones_iibb_base":   "0",
	        	"percepciones_iibb_alicuota": "0",
	        	"percepciones_iva":         "0",
	        	"percepciones_iva_base":    "0",
	        	"percepciones_iva_alicuota": "0",
	     		"exentos":                  "0",
	        	"impuestos_internos":       "0",
	        	"impuestos_internos_base":   "0",
	        	"impuestos_internos_alicuota": "0" ,
			"nogravados": 0,
			"total": 543.21,
			"cae": " ",
			"afip_codigo_barras" : " ",
			"afip_qr": "",
			"vencimiento_cae": "",
			"vencimiento_pago": "23\/05\/2021",
			"external_reference": "Lun141",
			"tags": [
				"etiqueta1",
				"etiqueta2"
				],
			"status": "APROBADO Y EN COLA. SE EMITE EL 16\/03\/2022",
			"ctacte_status": "",
			"comprobante_pdf_url": ""
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
A partir del 01/05/2022, está consultá comenzará a ser paginada, con un límite máximo de registros por página de 3,000.&#x20;
{% endhint %}

#### Ejemplo de JSON a enviar para consultar por fecha un comprobante:

Tipo de datos: **JSON**\
Charset: **UTF-8**

```
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
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
|     limite     | Valor numérico entero. Mínimo esperado: 0 Máximo: 3000 |

#### Estructura de "Comprobante":

| `operacion` | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p> |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `fecha`     | <p>Campo fecha en formato dd/mm/aaaa<br><strong>Ejemplo: 20/03/2022</strong></p>                                                                                                      |

## ¿Cómo realizar una consulta avanzada, por rango de números?

Ésta búsqueda te permite obtener todos los comprobantes enviados, ya sea porque se han emitido o porque se encuentren en la cola de facturación, dentro de un rango numérico.&#x20;

Debés tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

{% hint style="info" %}
A partir del 01/05/2022, está consultá comenzará a ser paginada, con un límite máximo de registros por página de 3,000.&#x20;
{% endhint %}

#### Detalle de los atributos a enviar:

|    Atributo    |                    Valores esperados                   |
| :------------: | :----------------------------------------------------: |
| busqueda\_tipo |          Campo alfanumérico esperado: "**TN**"         |
|   comprobante  |         Objeto según se detalla a continuación         |
|     pagina     |        Valor numérico entero. Mínimo esperado: 0       |
|     limite     | Valor numérico entero. Mínimo esperado: 0 Máximo: 3000 |

#### Estructura de "Comprobante":

| `tipo`         | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`    | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta`  | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero_desde` | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |
| `numero_hasta` | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |

#### Ejemplo del JSON a enviar :

```
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
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

## ¿Cómo realizar una consulta avanzada, por external reference?

{% hint style="info" %}
Ésta consulta estará disponible a partir del 01/04/2022&#x20;
{% endhint %}

Ésta búsqueda te permite obtener todos los comprobantes enviados, ya sea porque se han emitido o porque se encuentren en la cola de facturación, de una determinada external\_reference.&#x20;

Debés tener en cuenta que  la información obtenida, será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso y  el ordenamiento de los datos que te devuelve es: del último emitido al primero.&#x20;

#### Detalle de los atributos a enviar:

|    Atributo    |                    Valores esperados                   |
| :------------: | :----------------------------------------------------: |
| busqueda\_tipo |       Campo alfanumérico esperado: "**EXT\_REF**       |
|   comprobante  |         Objeto según se detalla a continuación         |
|     pagina     |        Valor númerico entero. Mínimo esperado: 0       |
|     limite     | Valor númerico entero. Mínimo esperado: 0 Máximo: 3000 |

#### Estructura de "Comprobante":

| `external_reference` | Campo alfanumérico. Longitud mínima: 1 carácter                                                                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`          | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p> |



#### Ejemplo del JSON a enviar :

```
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"busqueda_tipo": "EXT_REF",
 "pagina" : 0,
 "limite": 100 ,
"comprobante": {
		"external_reference": "DD2F1F1",
		"operacion": "V"
	}
} 
```

