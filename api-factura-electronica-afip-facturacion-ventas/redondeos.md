---
description: Conoce que tipo de redondeos se aplican en TusFacturasAPP.
icon: input-numeric
---

# Redondeos

TusFacturasAPP recalcula los totales de cada comprobante a partir de los ítems que envías, y esos totales son los que se informan a ARCA. Si tu sistema calcula los totales con otro criterio de redondeo, pueden aparecer diferencias de centavos entre tu comprobante y lo informado.

Recalculamos porque el servicio de facturación de ARCA (WSFEv1) no recibe el detalle de los ítems, sino solo los subtotales por alícuota y los impuestos.

Para evitar diferencias, calcula los totales con estas reglas:

| Concepto                 | Decimales | Cómo se calcula                                                                                                                                                                                                                                                      |
| ------------------------ | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Precio unitario del ítem | 3 máximo  | Lo envías vos. Si mandas más de 3 decimales, el cálculo los usa todos pero el PDF muestra el precio redondeado a 3. Entonces quien revise el PDF puede ver que cantidad × precio no da exactamente el importe del ítem. **Recomendamos enviar siempre 3 decimales.** |
| Subtotal por alícuota    | 2         | Suma de precio final de cada item sin IVA ni impuestos de esa alícuota, redondeado a 2 decimales con Round Half Even.                                                                                                                                                |
| IVA por alícuota         | 2         | Subtotal de cada importe de IVA redondeado a 2 decimales con Round Half Even.                                                                                                                                                                                        |
| Total del comprobante    | 2         | Suma de los subtotales y los impuestos, redondeado a 2 decimales con Round Half Even.                                                                                                                                                                                |

**Round Half Even** (redondeo bancario) es el método que exige ARCA. Cuando el valor termina exactamente en 5, se redondea al dígito par más cercano:

| Valor  | Redondeado |
| ------ | ---------- |
| 66,165 | 66,16      |
| 66,115 | 66,12      |

***

{% hint style="info" %}
Antes de tomar cualquier decisión, consulta siempre con tu estudio contable para evitar posibles errores y asegurarte de actuar conforme a la normativa vigente.
{% endhint %}

### **Cálculos sobre cada concepto/item:**

| Cálculo                           | Fórmula                                                                     | Ejemplo                      |
| --------------------------------- | --------------------------------------------------------------------------- | ---------------------------- |
| **Importe del item**              | Cantidad × Precio unitario                                                  | 2 × $50 = $100               |
| **Bonificación**                  | Importe ítem × % de bonificación                                            | $100 × 10% = $10             |
| **Precio final del ítem sin IVA** | Importe ítem − Bonificación                                                 | $100 − $10 = $90             |
| **Impuestos internos**            | Precio final del ítem sin IVA × % de impuestos internos                     | $90 × 20% = $18              |
| **IVA**                           | Precio final del ítem sin IVA × % de IVA _(sin incluir impuestos internos)_ | $90 × 21% = $18,90           |
| **Total del ítem**                | Precio final sin IVA + Impuestos internos + IVA                             | $90 + $18 + $18,90 = $126,90 |

### **¿Cómo se calcula el total de un comprobante?**

El cálculo de validación previa, que garantiza que el total que vos envias coincida con el que la plataforma recalcula, se realiza de la siguiente manera:

{% stepper %}
{% step %}
#### **Paso 1: Subtotal por alícuota**

Sumarizamos los ítems de cada alícuota de IVA: _cantidad × precio unitario sin IVA − bonificación, con los decimales que envies._  Usamos éste subtotal sin redondear para el cálculo de IVA.
{% endstep %}

{% step %}
#### **Paso 2: IVA por alícuota**

Calculamos el importe de cada alícuota de IVA sobre los subtotales obtenidos en el paso 1 y redondeamos cada resultado a **2 decimales**, aplicando el método **Round Half Even**

> ⚠️ **El IVA no se calcula ítem por ítem.** Se calcula sobre el subtotal de cada alícuota. Si en tu sistema sumas el IVA de cada ítem, pueden aparecer diferencias de centavos.
{% endstep %}

{% step %}
#### **Paso 3: Total del comprobante**

Sumamos los subtotales, otros impuestos y el IVA todos redondeados con 2 decimales Round Half Even y obtenemos el total.
{% endstep %}
{% endstepper %}

### ⚠️ **Tolerancia por redondeo ($0,03) hasta 31/01/2027:**

* **Hoy:** se acepta una diferencia de hasta $0,03.
* **Desde el 14/11/2026:** las cuentas API DEV funcionan sin tolerancia, para que puedas probar tu integración.
* **Desde el 01/02/2027:** no se aceptan diferencias de centavos. Lo que envíes tiene que coincidir exactamente con el recálculo de la plataforma.

### ¿Qué hacer si tengo diferencias con el precio final?

Como alternativas prácticas, podes consulta con tu estudio contable si te recomiendan enviar más decimales en los conceptos/items que facturas o agregar un concepto de **“Ajuste por redondeo”**, con un importe positivo o negativo, según corresponda. Tené en cuenta que estas son posibles alternativas que no necesariamente se adaptan a todos los negocios. **Desde TusFacturasAPP no brindamos asesoramiento contable ni impositivo**, por lo que te recomendamos consultar previamente con tu estudio contable cuál es la opción más adecuada para tu operatoria y qué alícuota de IVA corresponde aplicar al ajuste.

**Importante:** ARCA no permite emitir comprobantes con sub-totales negativos para las alícuotas «IVA No Gravado» o «Exento». Por este motivo, no podrás informar un ajuste negativo (por ejemplo, -$0,05) utilizando alguna de estas alícuotas, si no existe otro ítem de la misma alícuota que permita compensar ese importe y mantener el subtotal en cero o positivo.

### **Ejemplos prácticos:** &#x20;

Una factura cuyo precio final es $80 y el precio sin IVA del producto/servicio es de 66,165

| Concepto               | Sin redondear | Redondeado (half-even) |
| ---------------------- | ------------- | ---------------------- |
| Producto A (+ IVA 21%) | 66,165        |                        |
| Redondeo (+ IVA 21%)   | −0,050        |                        |
| **Subtotal sin IVA**   | **66,115**    | **66,12**              |
| IVA 21%                | 13,88415      | 13,88                  |
| **Total**              | **79,99915**  | **80,00** ✅            |

***

Una factura 2 cuyo precio final es $100 y tiene alícuotas de IVA diferentes en los conceptos

| Concepto                 | Sin redondear | Redondeado (half-even) |
| ------------------------ | ------------- | ---------------------- |
| Producto A (+ IVA 21%)   | 66,165        |                        |
| Producto B (+ IVA 10,5%) | 18,100        |                        |
| Redondeo (+ IVA 21%)     | −0,050        |                        |
| **Subtotal**             | **84,215**    | **84,22**              |
| IVA 21%                  | 13,88415      | 13,88                  |
| IVA 10,5%                | 1,9005        | 1,90                   |
| **Total**                | **99,99965**  | **100,00**             |

Cada IVA se calcula sobre la suma de los sub-totales de su propia alícuota, sin redondear:

* **IVA 21%:** (66,165 − 0,050) × 21% = 66,115 × 21% = 13,88415
* **IVA 10,5%:** 18,100 × 10,5% = 1,9005

***

Ejemplo donde vos envías 4 decimales para obtener el precio total esperado:

| Concepto               | Sin redondear   | Redondeado (half-even) | En el PDF  |
| ---------------------- | --------------- | ---------------------- | ---------- |
| Producto A (+ IVA 21%) | 96.694,2149     |                        | 96.694,215 |
| **Subtotal sin IVA**   | **96.694,2149** | **96.694,21**          | 96.694,21  |
| IVA 21%                | 20.305,785129   | 20.305,79              | 20.305,79  |
| **Total**              |                 | **117.000,00** ✅       | 117.000,00 |

El IVA se calcula sobre el subtotal sin redondear (96.694,2149 × 21%). El total es la suma del subtotal y el IVA ya redondeados: 96.694,21 + 20.305,79.

> **En el PDF, el precio del producto se ve con 3 decimales (96.694,215)**, pero el cálculo usa los 4 decimales enviados. Por eso, si alguien recalcula a mano con lo que ve en el PDF, puede obtener una diferencia de centavos: con 96.694,215 el total daría 117.000,01.

