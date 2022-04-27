---
description: >-
  Emití con la API de TusFacturas.app los siguientes comprobantes: Factura C /
  Nota de débito C / Nota de crédito C / Factura de crédito MiPyme C / Nota de
  crédito  MiPyme C / Nota de débito  MiPyme C
---

# Ejemplos de comprobantes tipo "C"

Los comprobantes de tipo "C", son aquellos que solo pueden ser emitidos por un CUIT cuya condición frente al IVA sea "Monotributo" o "Exento".

No sabes en qué momento emitir comprobantes de tipo **C**? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante C.&#x20;



A continuación podrás ver un ejemplo del JSON para emitir una FACTURA C. Podes consultar la documentación con referencia a cada campo, [desde aquí.](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante)

```
{
	"apitoken": "xxx",
	"cliente": {
		"documento_tipo": "CUIT",
		"condicion_iva": "M",
		"domicilio": "Av Sta Fe 23132",
		"condicion_pago": "210",
		"documento_nro": "3071229384",
		"razon_social": "VOUSYS",
		"provincia": "2",
		"email": "tusfacturas@vousys.com",
		"envia_por_mail": "N"
	},
	"apikey": "xxx",
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
		"total": 114.88,
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
        "impuestos_internos":       "0",
        "impuestos_internos_base":   "0",
        "impuestos_internos_alicuota": "0"
	},
	"usertoken": "xxxx"
}
```

## Ejemplo de: NOTA DE CRÉDITO C  - detallando comprobantes.

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO C, que [detalla los comprobantes asociados.](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas#envio-de-comprobantes-asociados-detallados)

Podés consultar la documentación con referencia a cada campo, [desde aquí.](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante)

```
{ "usertoken" :  "xxxxx", 
 "apikey"    :  "xxxx", 
 "apitoken"  :  "xxxxx",
 
"cliente": 
    {
         "documento_tipo":       "CUIT", 
         "documento_nro":        "30712293841", 
         "razon_social":         "VOUSYS", 
         "email":                "tusfacturas@vousys.com", 
         "domicilio":            "AV.LIBERTADOR 571", 
         "provincia":            "2", 
         "envia_por_mail":       "S", 
         "condicion_pago":       "211", 
         "condicion_iva":        "RI" 
    },
 
"comprobante": 
    {    "fecha":                    "20/03/2018", 
         "tipo":                     "NOTA DE CREDITO C", 
         "operacion":                "V", 
         "punto_venta":              "0002", 
         "numero":                   "00000012", 
         "periodo_facturado_desde":  "28/02/2018", 
         "periodo_facturado_hasta":  "28/02/2018", 
         "rubro":                    "Alimentos", 
         "rubro_grupo_contable":     "Alimentos",

"detalle":
             [
                  {
                     "cantidad":     "1", 
                     "producto":     
                         {"descripcion":     "EXENTO - AVENA INSTANTANEA x5 kg. al 21", 
                         "unidad_bulto":     "1", 
                         "lista_precios":     "Lista de precios API 3", 
                         "codigo":     "16098", 
                         "precio_unitario_sin_iva":     "100",
                         "alicuota": "-1"
                         },
                     "leyenda":     ""
                 } ,

                  {
                     "cantidad":     "1", 
                     "producto":     
                         {"descripcion":     "p2", 
                         "unidad_bulto":     "1", 
                         "lista_precios":     "Lista de precios API 3", 
                         "codigo":     "160398", 
                         "precio_unitario_sin_iva":     "10",
                         "alicuota": "-1"
                         },
                     "leyenda":     ""
                 }                  
  
             ],
         "bonificacion":             "0.00", 
         "leyenda_gral":             " ", 
         "percepciones_iibb":        "0",
         "percepciones_iibb_base":   "0",
         "percepciones_iibb_alicuota": "0",
         "percepciones_iva":         "0",
         "percepciones_iva_base":    "0",
         "percepciones_iva_alicuota": "0",
         "exentos":                  "0",
         "impuestos_internos":       "0",
         "impuestos_internos_base":   "0",
         "impuestos_internos_alicuota": "0",
         "total":                    "110" ,
          "comprobantes_asociados": [
                            {
                                "tipo_comprobante"   :    "FACTURA C",
                                 "punto_venta"  :    "145",
                                 "numero" : 12313,
                                 "comprobante_fecha": "07/07/2018",
                                 "cuit": 1111111111111     
                            } 
                       ]         
         
    } 
}
 
```

## Ejemplo de: NOTA DE DÉBITO C - asociando períodos

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO C, que no detalla los comprobantes asociados, sino que [indíca su período, tal como se especifica aquí.](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas#comprobantes-asociados-por-periodo)

Podés consultar la documentación con referencia a cada campo, [desde aquí.](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante)

```
{ "usertoken" :  "xxxxx", 
 "apikey"    :  "xxxx", 
 "apitoken"  :  "xxxxx",
 
"cliente": 
    {
         "documento_tipo":       "CUIT", 
         "documento_nro":        "30712293841", 
         "razon_social":         "VOUSYS", 
         "email":                "tusfacturas@vousys.com", 
         "domicilio":            "AV.LIBERTADOR 571", 
         "provincia":            "2", 
         "envia_por_mail":       "S", 
         "condicion_pago":       "211", 
         "condicion_iva":        "RI" 
    },
 
"comprobante": 
    {    "fecha":                    "20/03/2018", 
         "tipo":                     "NOTA DE CREDITO C", 
         "operacion":                "V", 
         "punto_venta":              "0002", 
         "numero":                   "00000012", 
         "periodo_facturado_desde":  "28/02/2018", 
         "periodo_facturado_hasta":  "28/02/2018", 
         "rubro":                    "Alimentos", 
         "rubro_grupo_contable":     "Alimentos",

"detalle":
             [
                  {
                     "cantidad":     "1", 
                     "producto":     
                         {"descripcion":     "EXENTO - AVENA INSTANTANEA x5 kg. al 21", 
                         "unidad_bulto":     "1", 
                         "lista_precios":     "Lista de precios API 3", 
                         "codigo":     "16098", 
                         "precio_unitario_sin_iva":     "100",
                         "alicuota": "-1"
                         },
                     "leyenda":     ""
                 } ,

                  {
                     "cantidad":     "1", 
                     "producto":     
                         {"descripcion":     "p2", 
                         "unidad_bulto":     "1", 
                         "lista_precios":     "Lista de precios API 3", 
                         "codigo":     "160398", 
                         "precio_unitario_sin_iva":     "10",
                         "alicuota": "-1"
                         },
                     "leyenda":     ""
                 }                  
  
             ],
         "bonificacion":             "0.00", 
         "leyenda_gral":             " ", 
         "percepciones_iibb":        "0",
         "percepciones_iibb_base":   "0",
         "percepciones_iibb_alicuota": "0",
         "percepciones_iva":         "0",
         "percepciones_iva_base":    "0",
         "percepciones_iva_alicuota": "0",
         "exentos":                  "0",
         "impuestos_internos":       "0",
         "impuestos_internos_base":   "0",
         "impuestos_internos_alicuota": "0",
         "total":                    "110" ,
          comprobantes_asociados_periodo: 
          {
            "fecha_desde"   :    "20/11/2020",
            "fecha_hasta"  :    "25/11/2020"  
        }     
         
    } 
}
 
```



### Datos a tener en cuenta:

{% hint style="info" %}
* Los comprobantes C, no llevan IVA.
* No sabes en qué momento emitir comprobantes de tipo C? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante C.&#x20;
* Si querés enviar un comprobante a un consumidor final, sin especificar su nombre y DNI, podes enviar:

&#x20;               Nro de documento = "0"

&#x20;              Tipo de documento = "OTRO"

&#x20;              En nombre, lo que tu contador/a te recomiende.

Tené en cuenta que ésto solo está permitido para comprobantes hasta ciertos montos.Consultá diariamente el monto actualizado por AFIP con el método de: [Consulta de topes CF](api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final.md)


{% endhint %}

### Ejemplo de llamada en PHP

```
// ENVIO REQUEST
$url ="https://www.tusfacturas.app/app/api/v2/facturacion/nuevo" ;
$ch = curl_init( $url );
curl_setopt( $ch, CURLOPT_POSTFIELDS,  json_encode ($facturacion_json) );
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
