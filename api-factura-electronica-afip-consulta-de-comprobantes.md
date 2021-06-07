---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para consultar y
  generar nuevamente el PDF de tus comprobantes.
---

# API Factura electrónica AFIP  - Comprobantes: Consulta y re-armado de PDF

Tipo de datos: **JSON**  
Charset: **UTF-8**

{% api-method method="post" host="https://www.tusfacturas.app/app/api/" path="v2/facturacion/consulta " %}
{% api-method-summary %}
Consulta individual de comprobante
{% endapi-method-summary %}

{% api-method-description %}
Mediante éste método podrás consultar la información asociada a un determinado comprobante.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="comprobante" required=true %}
**tipo:**    Campo numérico según tabla de referencia de Tipos de comprobantes\(\*\*\*\). Ejemplo: FACTURA B   
**operacion:**    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V   
**punto\_venta:**    Campo numérico entero. Longitud máxima 4 dígitos. Ejemplo: 3   
**numero:**    Campo numérico entero. Longitud máxima 8 digitos. Ejemplo: 4567   
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso.  
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus Credenciales de acceso.  
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus Credenciales de acceso.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de respuesta exitosa el campo "error" retornará una "S" y en caso de error una "N" y dentro de errores, una lista con cada uno de los errores encontrados.  
La estructura de los datos devueltos es igual a la envidada para la generación de los comprobantes.  
  
A continuación se visualiza un ejemplo del JSON retornado para el comprobante consultado.  
  
Importante:   
  
-  Los campos numéricos son retornados como número, salvo el CAE y el CUIT  
-  Para comprobantes tipo B, el precio ya incluye la alícuota de IVA calculada.  
  
{% endapi-method-response-example-description %}

{% tabs %}
{% tab title="JSON" %}
```
{
	"error": "N",
	"errores": [""]
	"rta": "OK",
	"cliente": {
		"documento_tipo": "DNI",
		"documento_nro": "1292963535 ",
		"razon_social": "Pirulo",
		"email": "test@test.com",
		"domicilio": "Av Sta Fe 123"
	},
	"comprobante": {
		"fecha": "28\/07\/2015",
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
		}, ],
		"bonificacion": 120,
		"subtotal_1":  380.45,
		"iva_alicuota": 21,
		"subtotal_2": 75,
		"iva_alicuota_2": 10.5,
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
		"afip_qr
		"afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
		"afip_qr": "https:\/\/www.afip.gob.ar\/fe\/qr\/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjAyMS0wNi0wNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjEwIiwidGlwb0NtcCI6MSwibnJvQ21wIjoiMDAwMDAwNzgiLCJpbXBvcnRlIjoiMDAwMDAwMDAwMzA4NS41MCIsIm1vbmVkYSI6IlBFUyIs ",
		"vencimiento_cae": "07\/08\/2015",
		"vencimiento_pago": "27\/08\/2015",
		"comprobante_pdf_url": "https://www.dominio.com/00000006.pdf",
	}
}
```
{% endtab %}

{% tab title="Plain Text" %}
```

```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Los datos devueltos por éste método mantienen la misma estructura que los enviados para generar un comprobante.
{% endhint %}

### Ejemplo de JSON a enviar para consultar un comprobante:

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}

```

{% api-method method="post" host="https://www.tusfacturas.app/app/api/v2" path="/facturacion/consulta\_avanzada" %}
{% api-method-summary %}
Consulta de comprobantes por fecha
{% endapi-method-summary %}

{% api-method-description %}
Mediante ésta consulta podrás obtener todos los comprobantes emitidos en una determinada fecha. La consulta está limitada a retornar como máximo 3,000 registros y la información obtenida será la relacionada al punto de venta desde el cual estás realizando la consulta.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="busqueda\_tipo" type="string" required=true %}
Se deberá enviar el valor "F"
{% endapi-method-parameter %}

{% api-method-parameter name="comprobante" type="object" required=true %}
Un objeto con los siguientes atributos:   
**fecha**:  en formato dd/mm/aaaa  
**operacion**: Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Devuelve un array con cada "comprobante". Misma estructura de datos devuelta en el metodo de consulta individual.
{% endapi-method-response-example-description %}

```
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
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
			"subtotal_1":  380.45,
			"iva_alicuota": 21,
			"subtotal_2": 75,
			"iva_alicuota_2": 10.5,
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
			"subtotal_1":  380.45,
			"iva_alicuota": 21,
			"subtotal_2": 75,
			"iva_alicuota_2": 10.5,
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
			"comprobante_pdf_url": "https://www.dominio.com/00000006.pdf"
		}
	}
	]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo de JSON a enviar para consultar por fecha un comprobante:

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"busqueda_tipo": "F",
"comprobante":  {
                "fecha":     "23/05/2021",
                "operacion": "V" 
        }
}
```

{% api-method method="post" host="https://www.tusfacturas.app/app/api/v2" path="/facturacion/consulta\_avanzada" %}
{% api-method-summary %}
Consulta de comprobantes por rango de números
{% endapi-method-summary %}

{% api-method-description %}
Mediante ésta consulta podrás obtener hasta 3,000 comprobantes  por consulta y la información obtenida será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="busqueda\_tipo" type="string" required=true %}
Se deberá enviar el valor "TN"
{% endapi-method-parameter %}

{% api-method-parameter name="comprobante" type="string" required=true %}
Se debera enviar un objeto con los siguientes atributos:  
**tipo**: Campo numérico según tabla de referencia de Tipos de comprobantes\(_\*_\). Ejemplo: FACTURA B operacion: Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V **punto\_venta**: Campo numérico entero. Longitud máxima 4 digitos. Ejemplo: 3 **numero\_desde**: Campo numérico entero. Longitud máxima 8 digitos. Ejemplo: 4567 **numero\_hasta**: Campo numérico entero. Longitud máxima 8 dígitos. Ejemplo: 4567
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Devuelve un array con cada "comprobante". Misma estructura de datos devuelta en el metodo de consulta individual.
{% endapi-method-response-example-description %}

```
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
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
			"punto_venta": 10,
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
			"subtotal_1":  380.45,
			"iva_alicuota": 21,
			"subtotal_2": 75,
			"iva_alicuota_2": 10.5,
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
			"punto_venta": 10,
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
			"subtotal_1":  380.45,
			"iva_alicuota": 21,
			"subtotal_2": 75,
			"iva_alicuota_2": 10.5,
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
			"comprobante_pdf_url": "https://www.dominio.com/00000006.pdf"
		}
	}
	]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del json a enviar para consultar comprobantes por rango de números:

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"busqueda_tipo": "TN",
"comprobante": {
		"tipo": "FACTURA A",
		"operacion": "V",
		"punto_venta": "00010",
		"numero_desde": "00000001",
		"numero_hasta": "00000300"
	}
}
```

## Regenear PDF

Mediante éste método podrás regenerar los archivos pdf

{% api-method method="post" host="https://www.tusfacturas.app/app/api/" path="v2/facturacion/regenerar\_pdf " %}
{% api-method-summary %}
Regenerar PDFs
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="usertoken" type="string" required=false %}
tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=false %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="comprobante" required=true %}
**tipo**    Campo numérico según tabla de referencia de Tipos de comprobantes\(\*\*\*\). Ejemplo: FACTURA B   
**operacion**    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V   
**punto\_venta**    Campo numérico entero. Longitud máxima 4 digitos. Ejemplo: 3   
**numero**    Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante. Ejemplo: 4567
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Regenera el PDF y te devuelve la URL del archivo
{% endapi-method-response-example-description %}

```
{
"error" :  "N",
"comprobante_pdf_url"    :  "http://www.prueba.com"
}

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON a enviar para regenerar el pdf

{% code title="JSON" %}
```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}


```
{% endcode %}

## Estructura de "Comprobante":

| `tipo` | Campo numérico según tabla de referencia de [Tipos de comprobantes\(\*\*\*\)](https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes). **Ejemplo: FACTURA B** |
| :--- | :--- |
| `operacion` | Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\).  Valores Permitidos: **V, C** **Ejemplo: V** |
| `punto_venta` | Campo numérico entero. Longitud máxima 4 digitos. **Ejemplo: 3** |
| `numero` | Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante. **Ejemplo: 4567** |

