---
description: >-
  API AFIP/ARCA para emitir comprobantes con bonificacione. Ideal para pymes que
  necesitan aplicar descuentos. Ejemplos incluidos. Confiable desde 2015. ¡Los
  desarrolladores la aman!
---

# Ejemplos con bonificaciones

### ¿Cómo aplicar bonificaciones a nivel producto?

Para aplicar un descuento a un producto, simplemente ingresa el porcentaje deseado en el campo "bonificacion\_porcentaje" dentro de cada "producto" . Es importante tener en cuenta que las bonificaciones están sujetas al Impuesto al Valor Agregado (IVA).

**Ejemplo:**

Si un producto tiene un precio base de $100 y se aplica una bonificación del 20% con una alícuota de IVA del 21%, el cálculo sería el siguiente:

* Descuento: $100 \* 20% = $20
* Precio con descuento (sin IVA): $100 - $20 = $80
* Precio con descuento (con IVA): $100 - $20 = $80 \* 21%  = $96.80

### Ejemplo de "Factura A" AFIP/ARCA con bonificación a nivel producto

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
      "condicion_iva":"RI"
   }, 
    "comprobante": {
        "external_reference": "0306-0301",
        "tags": [
            "etiqueta1",
            "etiqueta2"
        ],
        "tipo": "FACTURA A",
        "operacion": "V",
        "punto_venta": "10",
        "fecha": "14/11/2024",
        "vencimiento": "26/12/2024",
        "idioma": 1,
        "numero": 0,
        "moneda": "PES",
        "cotizacion": 3,
        "periodo_facturado_desde": "",
        "periodo_facturado_hasta": "",
        "rubro": "Deudores Varios",
        "rubro_grupo_contable": "Ventas",
        "detalle": [
            {
                "cantidad": 1,
                "afecta_stock": "N",
                "leyenda": " Color rojo",
                "producto": {
                    "codigo": "LAPICERA1",
                    "descripcion": "LAPICERAS BIC",
                    "actualiza_precio": "N",
                    "unidad_bulto": 1,
                    "lista_precios": "LAPICERAS",
                    "precio_unitario_sin_iva": 100,
                    "impuestos_internos_alicuota": 0,
                    "alicuota": 21,
                    "unidad_medida": 7
                },
                "actualiza_precio": "S",
                "bonificacion_porcentaje": 20
            }
        ],
        "abono": "N",
        "abono_frecuencia": 1,
        "abono_hasta": "11\/2024",
        "abono_actualiza_precios": "N",
        "bonificacion": 0,
        "leyenda_gral": "",
        "comentario": "", 
        "total": 96.8,
        "pagos": {
            "formas_pago": [
                {
                    "descripcion": "MercadoPago",
                    "importe": 50
                },
                {
                    "descripcion": "Pago con especies",
                    "importe": 20
                }
            ],
            "total": 70
        }
    } 
}
    
```



### Ejemplo de "Factura A" AFIP/ARCA con bonificación monetaria a nivel comprobante

Para aplicar un descuento a un comprobante, simplemente ingresa el monto exacto que deseas descontar en el campo "bonificacion" del bloque "comprobante".&#x20;

Es importante tener en cuenta que el Impuesto al Valor Agregado (IVA) se calcula sobre el subtotal luego de aplicar el descuento.

**Ejemplo:**

Si un producto tiene un precio base de $100 y se aplica una bonificación de $20 con una alícuota de IVA del 21%, el cálculo sería el siguiente:

* Precio con descuento (sin IVA): $100 - $20 = $80
* Precio con descuento (con IVA): $100 - $20 = $80 \* 21%  = $96.80

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
      "condicion_iva":"RI"
   }, 
    "comprobante": {
        "external_reference": "0306-0301",
        "tags": [
            "etiqueta1",
            "etiqueta2"
        ],
        "tipo": "FACTURA A",
        "operacion": "V",
        "punto_venta": "10",
        "fecha": "14/11/2024",
        "vencimiento": "26/12/2024",
        "idioma": 1,
        "numero": 0,
        "moneda": "PES",
        "cotizacion": 3,
        "periodo_facturado_desde": "",
        "periodo_facturado_hasta": "",
        "rubro": "Deudores Varios",
        "rubro_grupo_contable": "Ventas",
        "detalle": [
            {
                "cantidad": 1,
                "afecta_stock": "N",
                "leyenda": " Color rojo",
                "producto": {
                    "codigo": "LAPICERA1",
                    "descripcion": "LAPICERAS BIC",
                    "actualiza_precio": "N",
                    "unidad_bulto": 1,
                    "lista_precios": "LAPICERAS",
                    "precio_unitario_sin_iva": 100,
                    "impuestos_internos_alicuota": 0,
                    "alicuota": 21,
                    "unidad_medida": 7
                },
                "actualiza_precio": "S",
                "bonificacion_porcentaje": 0
            }
        ],
        "abono": "N",
        "abono_frecuencia": 1,
        "abono_hasta": "11\/2024",
        "abono_actualiza_precios": "N",
        "bonificacion": 20,
        "leyenda_gral": "",
        "comentario": "",
         
        "total": 96.8,
        "pagos": {
            "formas_pago": [
                {
                    "descripcion": "MercadoPago",
                    "importe": 50
                },
                {
                    "descripcion": "Pago con especies",
                    "importe": 20
                }
            ],
            "total": 70
        }
    } 
}
    
```



TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
