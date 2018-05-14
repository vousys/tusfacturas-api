---
description: Ejemplo JSON de para comprobantes tipo A
---

# Factura A / Nota de débito A / Nota de crédito A

```text

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
         "condicion_pago":       "0", 
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
         "percepciones_iva":         "0", 
         "exentos":                  "0", 
         "nogravados":               "0", 
         "impuestos_internos":       "0", 
         "total":                    "112.1" 
    } 
}
 
```

