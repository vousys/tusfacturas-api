---
description: Conoce que tipo de redondeos se aplican en TusFacturasAPP.
icon: input-numeric
---

# Redondeos

TusFacturasAPP gestiona los precios unitarios de los productos/items con **3 decimales** y los totales finales con **2 decimales**, aplicando el método de redondeo **"Round Half Even"** (redondeo bancario), siguiendo estrictamente los lineamientos de ARCA.

***

**¿Cómo se calcula el total?**

El cálculo de validación previa, que garantiza que el total que vos envias coincida con el que la plataforma recalcula, se realiza en cuatro pasos:

1. **Sumarizamos** todos los ítems (cantidad × precio unitario sin IVA) con los decimales tal como resultan del cálculo. Recorda que debes enviarlos con 3 decimales maximo, sin embargo no rechazamos aquellas ventas que ingresen con mas decimales.
2. **Redondeamos el subtotal sin IVA a 2 decimales** usando Round Half Even.
3. **Aplicamos el IVA** sobre esos subtotales ya redondeados y redondeamos el importe resultante a 2 decimales usando Round Half Even.
4. **Sumamos** subtotales e IVA para obtener el total del comprobante.

⚠️ **El IVA no se calcula línea por línea.** No se suma el IVA de cada ítem individualmente: se calcula sobre el subtotal acumulado. Tenelo en cuenta al verificar si el total coincide con tus propios cálculos, ya que calcular por ítem puede generar diferencias de centavos.

⚠️ **Tolerancia por redondeo ($0,03):**

Admitimos una discrepancia de hasta $0,03 entre el total enviado en el payload y el cálculo interno de la plataforma. En estos casos, el comprobante PDF conservará el total enviado por tu sistema, mientras que ante ARCA se declarará el importe recalculado por nuestra plataforma, por lo que recomendamos enviar la información de acuerdo a lo informado.

{% hint style="warning" %}
A partir del **01/02/2027**, no se admitirán diferencias de centavos. Los valores que envíes deberán coincidir exactamente con los resultados del recálculo realizado por la plataforma. Por tal motivo, desde el **14/11/2026** todas las cuentas del servicio **API DEV** comenzarán a trabajar con tolerancia cero. De esta manera, podras realizar los ajustes necesarios y comprobar que tu integración cumple con las nuevas validaciones antes de que entren en vigencia en el entorno productivo.
{% endhint %}



***

#### **Ejemplos prácticos:**

**Ejemplo práctico**

El siguiente ejemplo muestra una factura de 3 ítems con alícuota de IVA 21%. Los precios unitarios tienen un máximo de 3 decimales.

| Descripción | Cantidad | Precio unitario s/IVA | Cant × Precio s/IVA |
| ----------- | -------- | --------------------- | ------------------- |
| Producto A  | 3,00     | 150,250               | 450,750             |
| Producto B  | 2,50     | 120,050               | 300,125             |
| Producto C  | 2,00     | 124,875               | 249,750             |

**Resultado del cálculo:**

| Paso                                                 | Importe                 |
| ---------------------------------------------------- | ----------------------- |
| **1. Suma de los ítems** (Cant × Precio s/IVA)       | $1.000,625              |
| **2. Subtotal sin IVA redondeado** (Round Half Even) | $1.000,62               |
| **3. IVA 21%** sobre $1.000,62                       | $210,1302 → **$210,13** |
| **4. Total del comprobante**                         | **$1.210,75**           |

El valor `1.000,625` queda exactamente en el punto medio entre `1.000,62` y `1.000,63`. Round Half Even redondea hacia el número par más cercano: como el dígito anterior es `2` (par), el subtotal queda en `1.000,62`. Con un redondeo tradicional hacia arriba el subtotal sería `1.000,63` y el total `1.210,76`, un centavo más.



**Ejemplo con múltiples conceptos**

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

