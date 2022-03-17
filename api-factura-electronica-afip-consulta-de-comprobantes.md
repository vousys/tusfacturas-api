---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para consultar
  los comprobantes emitidos desde la plataforma, ya sea por una búsqueda puntual
  o una búsqueda avanzada.
---

# Consulta simple de comprobantes



Mediante éste método, podrás consultar la información asociada a un determinado comprobante.

Tipo de datos: **JSON**\
Charset: **UTF-8**

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/consulta " method="post" summary="Consulta individual de comprobante" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="comprobante" required="false" type="object" %}
Un objeto según estructura que se detalla a continuación.


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

#### Estructura a enviar dentro del bloque: "Comprobante"

| `tipo`        | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero`      | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |

#### Ejemplo de JSON a enviar :

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



{% hint style="info" %}
Los datos devueltos por éste método mantienen la misma estructura que los enviados para generar un comprobante.
{% endhint %}

#### Ejemplo del JSON de respuesta:

La información que obtenés se devuelve estructurada de la misma manera que la enviaste, con el agregado de ciertos campos que se detallan a continuación

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
		"external_reference": "Lun141",
		"tags": [
				"etiqueta1",
				"etiqueta2"
				],
		"ctacte_status": "PAGO PARCIAL",
		"status": "EMITIDO",
		"afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
		"afip_qr": "https:\/\/www.afip.gob.ar\/fe\/qr\/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjAyMS0wNi0wNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjEwIiwidGlwb0NtcCI6MSwibnJvQ21wIjoiMDAwMDAwNzgiLCJpbXBvcnRlIjoiMDAwMDAwMDAwMzA4NS41MCIsIm1vbmVkYSI6IlBFUyIs ",
		"vencimiento_cae": "07\/08\/2015",
		"vencimiento_pago": "27\/08\/2015",
		"comprobante_pdf_url": "https://www.dominio.com/00000006.pdf",
	}
}
```

#### Campos devueltos que no forman parte del JSON que vos envias:

| Nombre del campo        | Info                                                                                                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| cae                     | Campo alfanumérico, con un espacio adicional, devuelto por AFIP, a modo e código de autorización electrónica de la transacción realizada                                                                                 |
| afip\_qr                | Campo alfanumérico, conteniendo el texto necesario para formar el QR                                                                                                                                                     |
| ctacte\_status          | Campo alfanumérico, conteniendo el estado del pago de ese comprobante dentro de la cuenta corriente. Los valores posibles son: PAGADA, IMPAGA , PAGO PARCIAL                                                             |
| status                  | Campo alfanumérico, conteniendo el estado de emisión de ese comprobante . Lo valores les son: "EMITIDO", "APROBADO Y EN COLA. SE EMITE EL dd/mm/aaaa", "EN COLA, ESPERANDO APROBACION", "ENVIADO A PROCESAR - CON ERROR" |
| afip\_codigo\_barras    | Campo alfanumérico, conteniendo el texto necesario para formar el código de barras de AFIP (legacy)                                                                                                                      |
| vencimiento\_cae        | Fecha enviada por AFIP al momento de autorizar el comprobante. Formato: dd/mm/aaaa                                                                                                                                       |
| vencimiento\_pago       | Fecha que indica la fecha de vencimiento del pago. Éste dato enviado por el cliente, o auto-calculado en base a la condición de pago estipulada en el perfil del cliente. Formato: dd/mm/aaaa                            |
| comprobante\__pdf_\_url | Campo alfanumérico que al pdf del comprobante.                                                                                                                                                                           |









