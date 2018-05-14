---
description: Ejemplo de JSON para generar comprobantes tipo C
---

# Factura C / Nota de débito C / Nota de crédito C

```text
{
	"apitoken": "kkakak208a17cdfc4e4741437baddaa6",
	"cliente": {
		"documento_tipo": "CUIT",
		"condicion_iva": "M",
		"domicilio": "Av Sta Fe 23132",
		"condicion_pago": "0",
		"documento_nro": "3071229384",
		"razon_social": "VOUSYS",
		"provincia": "2",
		"email": "tusfacturas@vousys.com",
		"envia_por_mail": "N"
	},
	"apikey": "1235",
	"comprobante": {
		"rubro": "Sevicios web",
		"percepciones_iva": 0,
		"tipo": "FACTURA C",
		"numero": 2134,
		"percepciones_iibb": 0,
		"bonificacion": 0,
		"operacion": "V",
		"detalle": [{
			"cantidad": 1,
			"producto": {
				"descripcion": "Hosting pagina web ",
				"codigo": 37,
				"lista_precios": "standard",
				"leyenda": "",
				"unidad_bulto": 1,
				"alicuota": 21,
				"precio_unitario_sin_iva": 114.88
			}
		}],
		"fecha": "28/03/2018",
		"rubro_grupo_contable": "Sevicios",
		"total": 139.0,
		"cotizacion": 1,
		"moneda": "PES",
		"punto_venta": 3,
		"impuestos_internos": 0
	},
	"usertoken": "a7ahdt5s7725d7fa4f4e63646bc169b"

```

