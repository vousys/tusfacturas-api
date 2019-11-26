---
description: >-
  Se recomienda leer los requerimientos y conceptos básicos en el Micrositio de
  AFIP (http://www.afip.gob.ar/facturadecreditoelectronica/default.asp)  y
  ademas, consultar con su contador/a.
---

# Factura de Crédito Electrónica MiPyme \(FCE\)

La particularidad de éstos tipos de comprobante es que requiere de manera obligatoria que se envie información asociada,  dentro del bloque de " [rg\_especiales](./#estructura-de-rg-especiales) ", ademas de que solo aplica para ciertos receptores a partir de cierto monto.

Por el momento AFIP cuenta con éstos datos a enviar:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Descripcion del campo</th>
      <th style="text-align:left">Id a enviar</th>
      <th style="text-align:left">&#xBF;Requerido?</th>
      <th style="text-align:left">Detalle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>CBU emisor</p>
      </td>
      <td style="text-align:left">2101</td>
      <td style="text-align:left">REQUERIDO</td>
      <td style="text-align:left">CBU nume&#x301;rico de 22 caracteres</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>Referencia Comercial</p>
      </td>
      <td style="text-align:left">23</td>
      <td style="text-align:left">OPCIONAL</td>
      <td style="text-align:left">Texto. puede identificar una o varias Referencias Comerciales segu&#x301;n
        corresponda - no repetir el valor.</td>
    </tr>
    <tr>
      <td style="text-align:left">Alias del emisor</td>
      <td style="text-align:left">2102</td>
      <td style="text-align:left">OPCIONAL</td>
      <td style="text-align:left">El valor correcto es un ALIAS alfanumerico Longitud de 6 a 20 caracteres,
        letras de la &apos;a&apos; a la &apos;Z&apos;, numeros del &apos;0&apos;
        al &apos;9&apos;, caracteres especiales: punto ( . ) o guion medio ( -
        )</td>
    </tr>
    <tr>
      <td style="text-align:left">Anulacion</td>
      <td style="text-align:left">22</td>
      <td style="text-align:left">REQUERIDO</td>
      <td style="text-align:left">Solo debe ser enviado para las Notas de cr&#xE9;dito/debito y el valor
        esperado es : S o N. Indica si el comprobante fue rechazado por el receptor.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
Ten en cuenta que éste tipo de comprobantes, luego requieren de un tratamiento especial gestionado desde la web de AFIP para su autorización/aceptación/anulación. Consultá con tu contador/a el procedimiento indicado en la ley
{% endhint %}

## Factura A 

```text

{
	"usertoken": "hagagay2y884e1405e26c03c85",
	"apikey": "1234",
	"apitoken": "asduasuya81238173189378921378",
	"cliente": {
		"documento_tipo": "CUIT",
		"documento_nro": "30712293841",
		"razon_social": "VOUSYS",
		"email": "tusfacturas@vousys.com",
		"domicilio": "AV.LIBERTADOR 571",
		"provincia": "2",
		"envia_por_mail": "S",
		"condicion_pago": "210",
		"condicion_iva": "RI"
	},
	"comprobante": {
		"fecha": "20/03/2018",
		"tipo": "FACTURA DE CREDITO ELECTRONICA MiPyME (FCE) A",
		"operacion": "V",
		"punto_venta": "0002",
		"numero": "00000012",
		"periodo_facturado_desde": "07/07/2019",
		"periodo_facturado_hasta": "07/07/2019",
		"rubro": "Alimentos",
		"rubro_grupo_contable": "Alimentos",
		"detalle": [ {
			"cantidad": "1",
			"producto": {
				"descripcion": "p2",
				"unidad_bulto": "1",
				"lista_precios": "Lista de precios API 3",
				"codigo": "160398",
				"precio_unitario_sin_iva": 100000000,
				"alicuota": "21"
			},
			"leyenda": ""
		}],
		"bonificacion": "0.00",
		"leyenda_gral": " ",
		"percepciones_iibb": "0",
		"percepciones_iibb_base": "0",
		"percepciones_iibb_alicuota": "0",
		"percepciones_iva": "0",
		"percepciones_iva_base": "0",
		"percepciones_iva_alicuota": "0",
		"exentos": "0", 
		"impuestos_internos": "0",
		"impuestos_internos_base": "0",
		"impuestos_internos_alicuota": "0",
		"total": "121000000",
        "rg_especiales":   
            {   "regimen" : "Factura de Crédito Electrónica MiPyMEs (FCE)",
                 "datos"  : 

                           [{
                               "id"      :    2101,
                               "valor"  :    "1234567890123456789011"
                            },
                            {
                              "id"      :    23,
                             "valor"  :    "Prueba"
                             } 
                ]
            }, 
	}
}

```

### Nota de crédito A

Las notas de crédito requieren que se envíe el bloque de "[Comprobantes asociados](./#estructura-de-comprobantes-asociados)" , con la particularidad de que éstos comprobantes asociados deben estar en la misma moneda que el comprobante que se está enviando a generar y la fecha del comprobante asociado tiene que ser igual o menor a la fecha del comprobante que se está autorizando.

Ademas, es importante recalcar que deben enviar dentro del bloque de "[rg\_especiales](./#estructura-de-rg-especiales)", el dato id \#22  con el valor S o N.

{% code title="JSON" %}
```text
{
	"usertoken": "hagagay2y884e1405e26c03c85",
	"apikey": "1234",
	"apitoken": "asduasuya81238173189378921378",
	"cliente": {
		"documento_tipo": "CUIT",
		"documento_nro": "30712293841",
		"razon_social": "VOUSYS",
		"email": "tusfacturas@vousys.com",
		"domicilio": "AV.LIBERTADOR 571",
		"provincia": "2",
		"envia_por_mail": "S",
		"condicion_pago": "0",
		"condicion_iva": "RI"
	},
	"comprobante": {
		"fecha": "20/03/2018",
		"tipo": "NOTA DE CREDITO ELECTRONICA MiPyME (FCE) A",
		"operacion": "V",
		"punto_venta": "0002",
		"numero": "00000012",
		"periodo_facturado_desde": "07/07/2019",
		"periodo_facturado_hasta": "07/07/2019",
		"rubro": "Alimentos",
		"rubro_grupo_contable": "Alimentos",
		"detalle": [ {
			"cantidad": "1",
			"producto": {
				"descripcion": "p2",
				"unidad_bulto": "1",
				"lista_precios": "Lista de precios API 3",
				"codigo": "160398",
				"precio_unitario_sin_iva": 100000000,
				"alicuota": "21"
			},
			"leyenda": ""
		}],
		"bonificacion": "0.00",
		"leyenda_gral": " ",
		"percepciones_iibb": "0",
		"percepciones_iibb_base": "0",
		"percepciones_iibb_alicuota": "0",
		"percepciones_iva": "0",
		"percepciones_iva_base": "0",
		"percepciones_iva_alicuota": "0",
		"exentos": "0", 
		"impuestos_internos": "0",
		"impuestos_internos_base": "0",
		"impuestos_internos_alicuota": "0",
		"total": "121000000",
        "rg_especiales":   
            {   "regimen" : "Factura de Crédito Electrónica MiPyMEs (FCE)",
                 "datos"  : 

                           [{
                               "id"      :    2101,
                               "valor"  :    "1234567890123456789011"
                            },
                            {
                              "id"      :    22,
                             "valor"  :    "S"
                             } 
                ]
            }, 
		"comprobantes_asociados": [{
			"tipo_comprobante": "FACTURA DE CREDITO ELECTRONICA MiPyME (FCE) A",
			"punto_venta": "3",
			"numero": 1,
			"comprobante_fecha": "07/07/2019",
			"cuit": 1111111111111
		}]
	}
}


```
{% endcode %}

{% hint style="info" %}
Ten en cuenta que TusFacturas.app no realiza validaciones con respecto a los datos enviados. Las validaciones se realizan exclusivamente del lado de AFIP, previa generación del comprobante.
{% endhint %}

### Algunas de las validaciones que realiza AFIP:

[  
](https://app.gitbook.com/@tusfacturas/s/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-electronica-afip-exportacion)

