---
description: Conoce que tipo de redondeos se aplican en TusFacturasAPP.
icon: input-numeric
---

# Redondeos

TusFacturasAPP gestiona los precios unitarios de los productos/items con **3 decimales** y los totales finales con **2 decimales**, aplicando el método de redondeo **"Round Half Even"** (redondeo bancario), siguiendo estrictamente los lineamientos de ARCA.

***

### **¿Cómo se calcula el total?**

El cálculo de validación previa para garantizar que el total que vos envias coincida con el total que la plataforma recalcula, se realiza en tres pasos:

1. **Sumarizamos** todos los ítems con los decimales tal como los envias en el JSON (en el PDF se verán redondeados a 3 decimales)
2. **Calculamos el subtotal sin IVA** de esa sumatoria
3. **Aplicamos el IVA** sobre ese subtotal

⚠️ **El IVA no se calcula línea por línea.** No se suma el IVA de cada ítem individualmente para determinar el total: se calcula sobre el subtotal acumulado. Esto es importante tenerlo en cuenta al verificar si el total del comprobante coincide con tus propios cálculos. Margen de tolerancia de diferencia entre el total informado por tu plataforma y nuestro cálculo interno = 1 centavo.

***

#### **Ejemplo práctico**

El siguiente ejemplo muestra una factura con múltiples ítems, cantidades con decimales y alícuota de IVA 21%. Todos los productos tienen nombres genéricos para simplificar la lectura.

| Descripción | Cantidad | Precio unitario s/IVA | Cant × Precio s/IVA |
| ----------- | -------- | --------------------- | ------------------- |
| Producto A  | 3.37     | 166.014,83            | 559.469,9771        |
| Producto B  | 0.50     | 94.664,41             | 47.332,205          |
| Producto A  | 4.50     | 166.014,83            | 747.066,735         |
| Producto B  | 0.50     | 94.664,41             | 47.332,205          |
| Producto C  | 0.50     | 49.176,41             | 24.588,205          |
| Producto A  | 6.75     | 166.014,83            | 1.120.600,103       |
| Producto B  | 0.50     | 94.664,41             | 47.332,205          |
| Producto A  | 3.37     | 166.014,83            | 559.469,9771        |
| Producto B  | 0.50     | 94.664,41             | 47.332,205          |
| Producto A  | 4.50     | 166.014,83            | 747.066,735         |
| Producto B  | 0.50     | 94.664,41             | 47.332,205          |
| Producto A  | 1.00     | 166.014,83            | 166.014,83          |
| Producto D  | 0.10     | 39.341,10             | 3.934,11            |
| Producto B  | 0.50     | 94.664,41             | 47.332,205          |
| Producto A  | 1.25     | 166.014,83            | 207.518,5375        |
| Producto B  | 0.50     | 94.664,41             | 47.332,205          |
| Producto D  | 0.10     | 39.341,10             | 3.934,11            |
| Producto E  | 6.00     | 22.050,00             | 132.300,00          |
| Producto F  | 0.12     | 24.588,13             | 2.950,5756          |
| Producto G  | 0.12     | 26.186,41             | 3.142,3692          |
| Producto H  | 1.89     | 104.500,22            | 197.505,4158        |
| Producto I  | 1.89     | 151.571,20            | 286.469,568         |
| Producto J  | 4.00     | 7.650,00              | 30.600,00           |
| Producto F  | 0.58     | 24.588,13             | 14.261,1154         |
| Producto G  | 0.58     | 26.186,41             | 15.188,1178         |

**Resultado del cálculo:**

|                                                    | Importe           |
| -------------------------------------------------- | ----------------- |
| **Subtotal sin IVA** (suma de Cant × Precio s/IVA) | $5.153.405,916    |
| **IVA 21%** aplicado sobre el subtotal             | $1.082.215,242    |
| **Total con IVA**                                  | $6.235.621,158    |
| **Total redondeado (Round Half Even)**             | **$6.235.621,16** |

El redondeo de `$6.235.621,158` a 2 decimales da `$6.235.621,16` porque el dígito en la tercera posición decimal es 8, por lo que redondea hacia arriba.

***

Para más detalle sobre cómo funcionan los redondeos y los precios sin IVA, consulta el artículo de ayuda: [Ajustes, redondeos y precios sin IVA](https://ayuda.tusfacturas.app/es/articles/12548047-redondeos-ajustes-y-precios-sin-iva).
