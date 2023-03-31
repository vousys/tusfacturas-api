---
description: >-
  Conocé cómo configurar tu cuenta aplicar las percepciones RG5329 en los
  comprobantes que emitas.
---

# FAQs | RG5329

Te sugerimos siempre consultar con tu contador o asesor impositivo antes de realizar ésta configuración.

### ¿Qué debes hacer?

#### 1. Configurá tu CUIT/PDV

Ingresá por nuestra plataforma web a menú: Mi espacio de trabajo > Mis CUITs / PDV y abrí el bloque: "4. Configurá si es agente de percepción o retención." .&#x20;

Deberás tildar la opción : "Si, es agente percepción de IVA RG 5329" y luego presionar "Guardar".\
Tené en cuenta podrás indicar que un CUIT/PDV aplica RG5329, solo si éste se encuentra enlazado con AFIP.



#### 2. Productos

Para que un producto sea pasible de percepción IVA 5329 debe tener tildado (dentro de su perfil de producto) el campo: "Si, aplica percepción de IVA a productos comprendidos en la RG5329" y no debe formar parte de abonos en curso.\
Actualizaciones masivas:\
Para agilizar la actualización de ésta información podes seleccionar todos aquellos productos que no formen parte de abonos en curso, tildarlos desde la grilla de productos y luego presionar el botón "Acciones masivas" > "Activar RG5329"



#### 3. Clientes

Para que un cliente sea sujeto pasible de percepción IVA 5329 debe tener tildado (dentro de su perfil de cliente) el campo: "Si, es sujeto pasible de percepción de IVA RG5329" y no debe poseer abonos en curso.\
Actualizaciones masivas:\
Para agilizar la actualización de ésta información podes seleccionar todos aquellos responsables inscriptos que no tengan abonos en curso, tildarlos desde la grilla de clientes y luego presionar el botón "Acciones masivas" > "Activar RG5329"



### ¿Cuando se aplica la percepción IVA 5329?

Para que puedas aplicar las percepciones IVA RG5329, se deben cumplir las siguientes condiciones:

1. Realizas una venta
2. El CUIT/PDV está enlazado con AFIP y tiene indicado "Si, es agente percepción de IVA RG 5329"
3. El cliente está marcado como "Si, es sujeto pasible de percepción de IVA RG5329"
4. El producto está marcado como "Si, aplica percepción de IVA a productos comprendidos en la RG5329"
5. Emitís un comprobante de tipo "A"
6. El importe total de las percepciones de IVA RG 5329, superan el mínimo impuesto por AFIP. (_Monto mínimo vigente al 26/03/2023 de $3,000)_&#x20;
7. La fecha de vigencia de la RG5329 (01/04/2023) es anterior o igual al día de la fecha
8. No podrás usar el servicio de integración con tiendas de E-commerce si aplicas percepciones de cualquier tipo
9. No podrás crear abonos que apliquen percepciones de cualquier tipo.
10. Solo podrás emitir ventas que apliquen a la RG5329 desde nuestra plataforma web y/o servicio API.

En el servicio API, la información relativa a la percepción RG5329 debe ser enviada en el bloque "tributos", teniendo en cuenta todas estas condiciones.



### ¿Cual es la alícuota que se aplica a la percepción IVA RG5329?

Cuando la alícuota de IVA de tu producto sea 21%, se aplica una alícuota de 3%\
Cuando la alícuota de IVA de tu producto sea 10,5%, se aplica una alícuota de 1.5%



### Qué debes modificar en el JSON

#### 1. Productos

Debes enviar los atributos:

* &#x20;"rg5329"  con el valor "S" &#x20;
* "actualiza\_precio" con valor "S".

Ej:

```json
{
"comprobante": ...
"detalle": [
         {
         "cantidad": "2",
         "afecta_stock": "N",
         "bonificacion_porcentaje": "0",
         "producto": {
            "descripcion": "Papel carta",
            "unidad_bulto": "1",
            "lista_precios": "MI LISTA DE PRECIOS",
            "codigo": "",
            "precio_unitario_sin_iva": 102000,
            "alicuota": 21,
            "impuestos_internos_alicuota": 0,
            "rg5329": "S",
            "unidad_medida": "7",
            "actualiza_precio": "S"
         },
         "leyenda": ""
      },
}
```



#### 2. Clientes

Debes enviar el atributo  "rg5329"  con el valor "S"

```json

{
	"cliente": {
		"documento_tipo": "CUIT",
		"documento_nro": "30716252430",
		"razon_social": "VYAR SRL",
		"email": "ssss@asdd.com",
		"domicilio": "No especificado",
		"provincia": "26",
		"envia_por_mail": "N",
		"condicion_pago": "214",
		"condicion_pago_otra": "Cobrado en ventanilla",
		"condicion_iva": "RI",
		"rg5329": "S"
	},
}


```



#### 3. Tributos

Debes enviar el bloque "tributos", como se muestra en el ejemplo de una [factura A](api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-factura-nota-de-debito-b-nota-de-credito-bb.md).

Obtené desde las tablas de referencia, los valores posibles para los atributos: "[tipo de percepción](parametros/tablas-de-referencia.md#bloque-tributos-greater-than-tipos-de-percepcion-a-aplicar)" y "[régimen de percepción](parametros/tablas-de-referencia.md#bloque-tributos-greater-than-regimen-de-percepcion)"

```json
{
    "comprobante" : {
    
        "tributos":[
         {
            "tipo" : 6,
            "regimen": 3,
            "base_imponible": 204000,
            "alicuota": 3,
            "total": 6120
            
         },
	 {
            "tipo" : 6,
            "regimen": 3,
            "base_imponible": 200300,
            "alicuota": 1.5,
            "total": 3004.5
            
         },
				
         {
            "tipo":7,
            "regimen":5,
            "base_imponible":200,
            "alicuota":10,
            "total":20
         }
      ],
    
    }
}
```

