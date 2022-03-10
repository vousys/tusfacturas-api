---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para consultar y
  generar nuevamente el PDF de tus comprobantes.
---

# Consulta de comprobantes y re-armado de PDF

## Consulta individual de un comprobante

Tipo de datos: **JSON**\
Charset: **UTF-8**

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/consulta " method="post" summary="Consulta individual de comprobante" %}
{% swagger-description %}
Mediante éste método podrás consultar la información asociada a un determinado comprobante.
{% endswagger-description %}

{% swagger-parameter in="body" name="comprobante" required="false" %}
**tipo:**

\\

**operacion:**

\\

**punto\_venta:**

\\

**numero:**

\\
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus Credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus Credenciales de acceso.
{% endswagger-parameter %}
{% endswagger %}

{% hint style="info" %}
Los datos devueltos por éste método mantienen la misma estructura que los enviados para generar un comprobante.
{% endhint %}

### Ejemplo del JSON de respuesta:

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

### Ejemplo de JSON a enviar :

```
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

## Consultar comprobantes por fecha

{% swagger baseUrl="https://www.tusfacturas.app/app/api/v2" path="/facturacion/consulta_avanzada" method="post" summary="Consulta de comprobantes por fecha" %}
{% swagger-description %}
Mediante ésta consulta podrás obtener todos los comprobantes emitidos en una determinada fecha. La consulta está limitada a retornar como máximo 3,000 registros y la información obtenida será la relacionada al punto de venta desde el cual estás realizando la consulta.
{% endswagger-description %}

{% swagger-parameter in="body" name="busqueda_tipo" type="string" required="false" %}
Se deberá enviar el valor "F"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" type="object" required="false" %}
Un objeto con los siguientes atributos:

\\

**fecha**

: en formato dd/mm/aaaa

\\

**operacion**

: Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V
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

### Ejemplo de JSON a enviar para consultar por fecha un comprobante:

```
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

### Ejemplo del JSON de respuesta:

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

## Consulta de comprobantes por rango de números

{% swagger baseUrl="https://www.tusfacturas.app/app/api/v2" path="/facturacion/consulta_avanzada" method="post" summary="Consulta de comprobantes por rango de números" %}
{% swagger-description %}
Mediante ésta consulta podrás obtener hasta 3,000 comprobantes por consulta y la información obtenida será la relacionada al punto de venta desde el cual estás haciendo la solicitud, mediante tus credenciales de acceso.
{% endswagger-description %}

{% swagger-parameter in="body" name="busqueda_tipo" type="string" required="false" %}
Se deberá enviar el valor "TN"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" type="string" required="false" %}
Se debera enviar un objeto con los siguientes atributos:

\\

**tipo**

: Campo numérico según tabla de referencia de Tipos de comprobantes(

_\*_

). Ejemplo: FACTURA B

\\

**operacion**

: Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V

\\

**punto\_venta**

: Campo numérico entero. Longitud máxima 4 digitos. Ejemplo: 3

**numero\_desde**

: Campo numérico entero. Longitud máxima 8 digitos. Ejemplo: 4567

**numero\_hasta**

: Campo numérico entero. Longitud máxima 8 dígitos. Ejemplo: 4567
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
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar :

```
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

### Ejemplo del JSON de respuesta:

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

## Regeneración del archivo PDF

Mediante éste método podrás regenerar el archivos pdf.

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/regenerar_pdf " method="post" summary="Regeneración de PDFs" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="comprobante" required="false" %}
**tipo**

\\

**operacion**

\\

**punto\_venta**

\\

**numero**
{% endswagger-parameter %}

{% swagger-response status="200" description="Regenera el PDF y te devuelve la URL del archivo" %}
```
{
"error" :  "N",
"comprobante_pdf_url"    :  "http://www.prueba.com"
}
```
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar para regenerar el pdf

{% code title="JSON" %}
```
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

### Ejemplo del JSON de respuesta:

```
{
"error" :  "N",
"comprobante_pdf_url"    :  "http://www.prueba.com"
}
```

## Estructura de "Comprobante":

| `tipo`        | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero`      | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |
