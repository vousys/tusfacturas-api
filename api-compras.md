---
description: >-
  Optimiza tu proceso de compras con la API Compras y nuestro sistema ERP
  gestiona las compras y agiliza tu flujo de trabajo sin esfuerzo.
---

# API Compras

Para crear una compra debes enviar un request como el que envías para las ventas, tal como se especifica aqui:  [api-factura-electronica-afip-facturacion-ventas](api-factura-electronica-afip-facturacion-ventas/ "mention"), con las siguientes diferencias:&#x20;

### Datos del proveedor

En lugar de enviar el bloque "cliente" debes enviar el bloque "proveedor" con la misma información, como se ve a continuación:

```
{    
"proveedor": {
        "documento_tipo": "CUIT",
        "razon_social": "Pepsico",
        "email": "vosorio@vousys.com",
        "domicilio": "CONSTITUCION 178",
        "documento_nro": "30537647716",
        "provincia": 2, 
        "condicion_pago": 0,
        "condicion_pago_otra": 0, 
        "condicion_iva": "RI"
    }
}
```

### Productos

Si necesitas que los productos comprados se incorporen como un producto mas en tus listas de precios de venta, debes indicar el campo <mark style="color:purple;">"incluir\_lista\_precios\_venta": "S"</mark>, dentro de cada producto en el bloque "detalle", como se ve a continuación:

```json
"comprobante": 
{
        "detalle": [
            {
                "cantidad": 10,
		"incluir_lista_precios_venta": "S",
                "afecta_stock": "S", 
                "producto": {
	            "lista_precios": "flores",
		    "codigo": "MembrilloJ3",
		    "descripcion": "Membrillo Japones 3",
		    "actualiza_precio": "N",
                    "unidad_bulto": 1,
                    "precio_unitario_sin_iva": 20000,
                    "impuestos_internos_alicuota": 10,
                    "alicuota": 21,
                    "unidad_medida": 7
                },
                "actualiza_precio": "N",
                "bonificacion_porcentaje": 0
            }
        ],

}
```

\
Ejemplo completo de un JSON para generar una compra:

```json
{
    "usertoken": "XXXXXXX",
    "apikey": 0000,
    "apitoken": "XXXXXX",
    "comprobante": {
        "external_reference": "A1",
        "tags": [
            "etiqueta1",
            "etiqueta2"
        ],
        "tipo": "FACTURA A",
        "operacion": "C",
        "punto_venta": "15",
        "fecha": "10/07/2024",
        "vencimiento": "16/07/2024",
        "idioma": 1,
        "numero": 24,
        "moneda": "PES",
        "cotizacion": 1,
        "periodo_facturado_desde": "",
        "periodo_facturado_hasta": "",
        "rubro": "Deudores Varios",
        "rubro_grupo_contable": "COMPRAS",
        "detalle": [
            {
                "cantidad": 10,
		"incluir_lista_precios_venta": "S",
                "afecta_stock": "S", 
                "producto": {
	                "lista_precios": "flores",
			"codigo": "MembrilloJ3",
			"descripcion": "Membrillo Japones 3",
			"actualiza_precio": "N",
                        "unidad_bulto": 1,
                        "precio_unitario_sin_iva": 20000,
                        "impuestos_internos_alicuota": 10,
                        "alicuota": 21,
                        "unidad_medida": 7
                },
                "actualiza_precio": "N",
                "bonificacion_porcentaje": 0
            }
        ],
        "abono": "N",
        "bonificacion": 0,
        "leyenda_gral": " ",
        "comentario": "", 
        "tributos": [
            {
                "tipo": 6,
                "regimen": 1,
                "base_imponible": 1000,
                "alicuota": 3,
                "total": 30
            }
        ],
        "impuestos_internos": "500",
        "impuestos_internos_base": "5000",
        "impuestos_internos_alicuota": "10",
        "total": 242530,
        "pagos": {
            "formas_pago": [
                {
                    "descripcion": "MercadoPago",
                    "importe": "1000"
                },
                {
                    "descripcion": "Efectivo",
                    "importe": "1000"
                }
            ],
            "total": 2000
        }
    },
    "proveedor": {
        "documento_tipo": "CUIT",
        "razon_social": "Pepsico",
        "email": "",
        "domicilio": "CONSTITUCION 178",
        "documento_nro": "30537647716",
        "provincia": 2, 
        "condicion_pago": 0,
        "condicion_pago_otra": 0 
        "condicion_iva": "RI"
    }
}
```
