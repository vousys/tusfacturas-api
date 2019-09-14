---
description: >-
  FacturaB / Nota de débito B / Nota de crédito B / Factura de crédito MiPyme B
  / Nota de crédito  MiPyme B / Nota de débito  MiPyme B
---

# Comprobantes de tipo B

{% hint style="info" %}
Ten en cuenta, que en los comprobantes B, el IVA se suma al total del producto, pero no aparecerá desglozado en la factura, ya que tu cliente no lo puede discriminar. Vos debes enviarlo siempre SIN IVA el precio.
{% endhint %}

```text
{
	"apitoken": "kkakak208a17cdfc4e4741437baddaa6",
	"cliente": {
		"documento_tipo": "CUIT",
		"condicion_iva": "M",
		"domicilio": "Av Sta Fe 23132",
		"condicion_pago": "201",
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
		"tipo": "FACTURA B",
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
       "percepciones_iibb":        "0",
       "percepciones_iibb_base":   "0",
        "percepciones_iibb_alicuota": "0",
        "percepciones_iva":         "0",
        "percepciones_iva_base":    "0",
        "percepciones_iva_alicuota": "0",
        "exentos":                  "0",
        "nogravados":               "0",
        "impuestos_internos":       "0",
        "impuestos_internos_base":   "0",
        "impuestos_internos_alicuota": "0" 
	},
	"usertoken": "a7ahdt5s7725d7fa4f4e63646bc169b"
}
```

{% hint style="info" %}
Si queres enviar un comprobante a un consumidor final, sin especificar su nombre y DNI, podes enviar:

* Nro de documento = "0" 
* Tipo de documento = "OTRO"
* En nombre, lo que tu contador/a te recomiende. 

Ten en cuenta que ésto solo está permitido para comprobantes hasta ciertos montos \(En Julio 2019 el tope es de $10,000, pero éste valor puede sufrir modificaciones\).

 Envianos tu consulta a tusfacturas@vousys.com 
{% endhint %}

### Ejemplo de llamada en PHP

```text
// ENVIO REQUEST
$url ="https://www.tusfacturas.app/app/api/v2/facturacion/nuevo" ;
$ch = curl_init( $url );
curl_setopt( $ch, CURLOPT_POSTFIELDS, json_encode ($facturacion_json) );
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
$json_rta_curl =  json_decode(  curl_exec($ch) ) ;  
curl_close($ch);

// MUESTRO RESPUESTA
echo "<p>MENSAJE:". $json_rta_curl->rta."</p>"; 
echo "<p>Vencimiento del pago:".$json_rta_curl->vencimiento_pago."</p>"; 
echo "<p>CAE:".$json_rta_curl->cae."</p>"; 
echo "<p>Vencimiento del cae:".$json_rta_curl->vencimiento_cae."</p>"; 
echo "<p>Comprobante pdf url:".$json_rta_curl->comprobante_pdf_url."</p>"; 
echo "<p>error:". $json_rta_curl->error ."</p>"; 
echo "<p>errores:". implode("," , $json_rta_curl->errores) ."</p>"; 


```

