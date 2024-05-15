---
description: >-
  Emití con la API de facturación electrónica AFIP Argentina provista por
  TusFacturasApp, comprobantes AFIP de tipo "A"
---

# Ejemplos de comprobantes tipo "A"

Los comprobantes de tipo "A" (Factura A / Nota de débito A / Nota de crédito A / Factura de crédito MiPyme A / Nota de crédito MiPyme A / Nota de débito MiPyme A), son aquellos que solo pueden ser emitidos por un CUIT cuya condición frente al IVA sea "Responsable inscripto".

No sabes en qué momento emitir comprobantes de tipo **A**? Consultá [desde aquí](../que-tipos-de-comprobante-debo-puedo-emitir.md) quienes deben emitir un comprobante A.&#x20;

## Datos a tener en cuenta:

{% hint style="info" %}
A partir del 01-07-2021, todo comprobante A que se emita a un monotributista deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618"._ **Éste dato **<mark style="background-color:yellow;">**no debe ser enviado**</mark>** en el campo "leyenda\_gral", ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma.**


{% endhint %}

### Nota de Crédito A

#### ¿Qué es una nota de crédito electrónica?

Es un comprobante dígital legalmente equivalente a la [nota de crédito](https://www.tusfacturas.app/como-emitir-notas-de-credito-electronica-afip.html) en formato papel, que la reemplaza en la mayoría de las operaciones de quienes estén obligados u opten por su utilización.

#### Ejemplo de: NOTA DE CRÉDITO A  - detallando comprobantes.

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO A, que detalla los comprobantes asociados.

Podés consultar la documentación con referencia a cada campo, [desde aquí](api-factura-electronica-afip-notas-credito-debito.md).

```json
{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI",
      "rg5329":"N"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"NOTA DE CREDITO A",
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
               "alicuota":"-1",
               "rg5329":"N"
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
               "alicuota":"21",
               "rg5329":"N"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         {
            "tipo":6,
            "regimen":2,
            "base_imponible":100,
            "alicuota":10,
            "total":10
         },
         {
            "tipo":7,
            "regimen":5,
            "base_imponible":200,
            "alicuota":10,
            "total":20
         }
      ],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":"142.1",
      "comprobantes_asociados":[
         {
            "tipo_comprobante":"FACTURA A",
            "punto_venta":"145",
            "numero":12313,
            "comprobante_fecha":"07/07/2018",
            "cuit":1111111111111
         }
      ]
   }
}
```

### NOTA DE DEBITO A

#### ¿Qué es una nota de débito electrónica?

Es un comprobante dígital legalmente equivalente a la [nota de débito](https://www.tusfacturas.app/como-emitir-notas-de-debito-electronica-afip.html) en formato papel, que la reemplaza en la mayoría de las operaciones de quienes estén obligados u opten por su utilización.

#### Ejemplo de: NOTA DE DÉBITO A - asociando períodos

A continuación podrás ver un ejemplo del JSON para emitir una NOTA DE CRÉDITO A, que no detalla los comprobantes asociados, sino que [indíca su período, tal como se especifica aquí.](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas#comprobantes-asociados-por-periodo)

Podés consultar la documentación con referencia a cada campo, [desde aquí](api-factura-electronica-afip-notas-credito-debito.md).

```json
{
   "usertoken":"xxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI",
      "rg5329":"N"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "vencimiento":"26/03/2023",
      "tipo":"NOTA DE DEBITO A",
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
               "alicuota":"-1",
               "rg5329":"N"
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
               "alicuota":"21",
               "rg5329":"N"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         {
            "tipo":6,
            "regimen":2,
            "base_imponible":100,
            "alicuota":10,
            "total":10
         },
         {
            "tipo":7,
            "regimen":5,
            "base_imponible":200,
            "alicuota":10,
            "total":20
         }
      ],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":"142.1",
       "comprobantes_asociados_periodo": {
        "fecha_desde"   :    "20/11/2020",
        "fecha_hasta"  :    "25/11/2020"  
   }
}
```



## Ejemplo de FACTURA A&#x20;

A continuación podrás ver un ejemplo del JSON para emitir una FACTURA A que no aplica a la RG5329.

```json
{
   "usertoken":"xxxx",
   "apikey":"xxx",
   "apitoken":"xxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS TusFacturasAPP",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI"
   },
   "comprobante":{
      "fecha":"20/03/2018",
      "tipo":"FACTURA A",
      "vencimiento":"26/03/2023",
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
               "alicuota":"21",
               "rg5329":"N"
            },
            "leyenda":"Enviadas en cajas separadas"
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         {
            "tipo":6,
            "regimen":2,
            "base_imponible":100,
            "alicuota":10,
            "total":10
         },
         {
            "tipo":7,
            "regimen":5,
            "base_imponible":200,
            "alicuota":10,
            "total":20
         }
      ],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":"151",
      "comprobantes_asociados":[
         
      ]
   }
}
```

#### Ejemplo de cómo emitir una factura A que percibe IVA por la RG5329.&#x20;

Conocé cuándo aplicar la RG5329, desde nuestras [FAQs](../faqs-or-preguntas-frecuentes.md)

```json
{
   "usertoken":"xxxx",
   "apikey":"xxx",
   "apitoken":"xxxx",
   "cliente":{
      "documento_tipo":"CUIT",
      "documento_nro":"30712293841",
      "razon_social":"VOUSYS",
      "email":"a@a.com",
      "domicilio":"AV.LIBERTADOR 571",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"211",
      "condicion_iva":"RI",
      "rg5329":"S"
   },
   "comprobante":{
      "fecha":"26/03/2023",
      "vencimiento":"26/03/2023",
      "tipo":"FACTURA A",
      "operacion":"V",
      "punto_venta":"0002",
      "numero":"00000012",
      "periodo_facturado_desde":"28/02/2018",
      "periodo_facturado_hasta":"28/02/2018",
      "rubro":"Alimentos",
      "rubro_grupo_contable":"Alimentos",
      "detalle":[
         {
            "cantidad":"2",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"Papel carta",
               "unidad_bulto":"1",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":102000,
               "alicuota":21,
               "impuestos_internos_alicuota":0,
               "rg5329":"S",
               "unidad_medida":"7",
               "actualiza_precio":"S"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"Paneles solares",
               "unidad_bulto":"1",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":1000,
               "alicuota":21,
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"N"
            },
            "leyenda":""
         },
         {
            "cantidad":"1",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"Celulares",
               "unidad_bulto":"1",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":200300,
               "alicuota":10.5,
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"S",
               "rg5329":"S"
            },
            "leyenda":""
         }
      ],
      "bonificacion":"0.00",
      "leyenda_gral":" ",
      "tributos":[
         {
            "tipo":6,
            "regimen":3,
            "base_imponible":204000,
            "alicuota":3,
            "total":6120
         },
         {
            "tipo":6,
            "regimen":3,
            "base_imponible":200300,
            "alicuota":1.5,
            "total":3004.5
         },
         {
            "tipo":7,
            "regimen":5,
            "base_imponible":200,
            "alicuota":10,
            "total":20
         }
      ],
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "total":478526,
      "comprobantes_asociados":[
         
      ]
   }
}
```



### Ejemplo de llamada en PHP

```php
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

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).
