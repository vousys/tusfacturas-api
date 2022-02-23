---
description: >-
  Emití con la API de TusFacturas.app los siguientes comprobantes:  Factura A /
  Nota de débito A / Nota de crédito A / Factura de crédito MiPyme A / Nota de
  crédito  MiPyme A / Nota de débito  MiPyme A
---

# API - Factura electrónica AFIP | Comprobantes de tipo A



{% hint style="info" %}
A partir del 01-07-2021, todo comprobante A que se emita a un monotributista deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618"._ **Éste dato no debe ser enviado en el campo "leyenda\_gral", ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma.**
{% endhint %}

## Ejemplo de: NOTA DE CRÉDITO A

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO A, que detalla los comprobantes asociados.

Podés consultar la documentación con referencia a cada campo, [desde aquí.](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante)

```
{ "usertoken" :  "hagagay2y884e1405e26c03c85", 
 "apikey"    :  "1234", 
 "apitoken"  :  "asduasuya81238173189378921378",
 
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
         "tipo":                     "NOTA DE CREDITO A", 
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
                         "alicuota": "21"
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
         "total":                    "112.1" ,
          "comprobantes_asociados": [
                            {
                                "tipo_comprobante"   :    "FACTURA A",
                                 "punto_venta"  :    "145",
                                 "numero" : 12313,
                                 "comprobante_fecha": "07/07/2018",
                                 "cuit": 1111111111111     
                            } 
                       ]         
         
    } 
}
 
```

## Ejemplo de FACTURA A&#x20;

A continuación podrás ver un ejemplo del JSON para emitir una FACTURA A.

```
{ "usertoken" :  "hagagay2y884e1405e26c03c85", 
 "apikey"    :  "1234", 
 "apitoken"  :  "asduasuya81238173189378921378",
 
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
         "tipo":                     "FACTURA A", 
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
                         {
                         "descripcion":     "EXENTO - AVENA INSTANTANEA x5 kg. al 21", 
                         "unidad_bulto":     "1", 
                         "lista_precios":     "Lista de precios API 3", 
                         "codigo":     "16098", 
                         "precio_unitario_sin_iva":     "100",
                         "alicuota": "21"
                         },
                     "leyenda":     "Enviadas en cajas separadas"
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
         "total":                    "121" ,
          "comprobantes_asociados": []         
         
    } 
}
 
```

}

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
