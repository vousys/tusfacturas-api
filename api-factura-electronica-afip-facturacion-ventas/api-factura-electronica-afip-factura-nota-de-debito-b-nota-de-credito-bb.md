---
description: >-
  Emití con la API de facturación electrónica AFIP Argentina provista por
  TusFacturasApp, comprobantes AFIP de tipo "B"
---

# Ejemplos de comprobantes tipo "B"

Los comprobantes de tipo "B" (Factura B / Notas de débito B / Nota de crédito B / Factura de crédito MiPyme B / Notas de crédito MiPyme B / Nota de débito MiPyme B), son aquellos que solo pueden ser emitidos por un CUIT cuya condición frente al IVA sea "Responsable inscripto" y se emitan a un consumidor final o un exento en IVA. No sabes en qué momento emitir comprobantes de tipo **B**? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante B.&#x20;

### Datos a tener en cuenta:

{% hint style="info" %}
* En los comprobantes B el IVA se suma al total del producto, pero no aparecerá desglozado en la factura, ya que tu cliente no lo puede discriminar. Vos debes enviarlo siempre SIN IVA el precio.
* ¿No sabes en que momento emitir comprobantes de tipo B? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante B.&#x20;
* Si queres enviar un comprobante a un consumidor final, sin especificar su nombre y DNI, podes enviar:

&#x20;               Nro de documento = "0"

&#x20;              Tipo de documento = "OTRO"

&#x20;              En nombre, lo que tu contador/a te recomiende.

Tené en cuenta que ésto solo está permitido para comprobantes hasta ciertos montos. Consulta diariamente el monto actualizado por AFIP con el método de: [Consulta de topes CF](api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final.md)


{% endhint %}

### Ejemplo de Factura B

A continuación podrás ver un ejemplo del JSON para emitir una FACTURA B. Podes consultar la documentación con referencia a cada campo, [desde aquí](./).

```json
{
   "apitoken":"xxxx",
   "cliente":{
      "documento_tipo":"DNI",
      "condicion_iva":"CF",
      "domicilio":"Av Sta Fe 23132",
      "condicion_pago":"201",
      "documento_nro":"111132333",
      "razon_social":"Juan Pedro KJL",
      "provincia":"2",
      "email":"email@dominio.com",
      "envia_por_mail":"N",
       "rg5329": "N"
   },
   "apikey":"xxxx",
   "comprobante":{
      "rubro":"Sevicios web",
      "percepciones_iva":0,
      "tipo":"FACTURA B",
      "numero":2134,
      "bonificacion":0,
      "operacion":"V",
      "detalle":[
         {
            "cantidad":1,
            "afecta_stock":"S",
            "actualiza_precio":"S",
            "bonificacion_porcentaje":0,
            "producto":{
               "descripcion":"Hosting pagina web ",
               "codigo":37,
               "lista_precios":"standard",
               "leyenda":"",
               "unidad_bulto":1,
               "alicuota":21,
               "actualiza_precio":"S",
               "rg5329": "N",
               "precio_unitario_sin_iva":114.88
            }
         }
      ],
      "fecha":"28/03/2018",
      "vencimiento":"26/03/2023",
      "rubro_grupo_contable":"Sevicios",
      "total":139.0,
      "cotizacion":1,
      "moneda":"PES",
      "punto_venta":3,
      "tributos":[],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0"
   },
   "usertoken":"xxxx"
}n
```

## Ejemplo de: NOTA DE CRÉDITO B  - detallando los comprobantes que anulas.

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO A, que detalla los comprobantes asociados.

Podés consultar la documentación con referencia a cada campo, [desde aquí](api-factura-electronica-afip-notas-credito-debito.md).

```json
{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"DNI",
      "documento_nro":"12345678",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"CF"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"NOTA DE CREDITO B",
      "operacion":"V",
      "punto_venta":"0002",
      "numero":"00000012",
      "periodo_facturado_desde":"28/02/2018",
      "periodo_facturado_hasta":"28/02/2018",
      "rubro":"Alimentos",
      "rubro_grupo_contable":"Alimentos",
      "detalle":[
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"EXENTO - AVENA INSTANTANEA x5 kg. al 21",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"16098",
               "precio_unitario_sin_iva":"100",
               "alicuota":"-1"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "producto":{
               "descripcion":"p2",
               "unidad_bulto":"1",
               "lista_precios":"Lista de precios API 3",
               "codigo":"160398",
               "precio_unitario_sin_iva":"10",
               "alicuota":"21"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         
      ],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":"112.1",
      "comprobantes_asociados":[
         {
            "tipo_comprobante":"FACTURA B",
            "punto_venta":"145",
            "numero":12313,
            "comprobante_fecha":"07/07/2018",
            "cuit":1111111111111
         }
      ]
   }
}
```

## Ejemplo de: NOTA DE DÉBITO B - asociando períodos

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO B, que no detalla los comprobantes asociados, sino que indíca su período.

Podés consultar la documentación con referencia a cada campo [desde aquí](api-factura-electronica-afip-notas-credito-debito.md).

```json
{ "usertoken" :  "xxxxx", 
 "apikey"    :  "xxxx", 
 "apitoken"  :  "xxxxx",
 
"cliente": 
    {
         "documento_tipo":       "DNI", 
         "documento_nro":        "12345678", 
         "razon_social":         "VOUSYS TusFacturasAPP", 
         "email":                "a@a.com", 
         "domicilio":            "AV.LIBERTADOR 571", 
         "provincia":            "2", 
         "envia_por_mail":       "S", 
         "condicion_pago":       "211", 
         "condicion_iva":        "CF" 
    },
 
"comprobante": 
    {    "fecha":                    "20/03/2018", 
         "vencimiento":              "26/03/2023",
         "tipo":                     "NOTA DE DEBITO B", 
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
         "tributos":                [],
         "impuestos_internos":       "0",
         "impuestos_internos_base":   "0",
         "impuestos_internos_alicuota": "0",
         "total":                    "112.1" ,
      "comprobantes_asociados_periodo": {
        "fecha_desde"   :    "20/11/2020",
        "fecha_hasta"  :    "25/11/2020" 
    } 
  } 
}

```

### Ejemplo de llamada en PHP

```php
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



TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).
