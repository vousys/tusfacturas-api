---
description: Conoce que tipo de redondeos se aplican en TusFacturasAPP.
icon: input-numeric
---

# Redondeos

TusFacturasAPP recalcula los totales de cada comprobante a partir de los ítems que envías, y esos totales son los que se informan a ARCA. Si tu sistema calcula los totales con otro criterio de redondeo, pueden aparecer diferencias de centavos entre tu comprobante y lo informado.

Recalculamos porque el servicio de facturación de ARCA (WSFEv1) no recibe el detalle de los ítems, sino solo los subtotales por alícuota y los impuestos.

Para evitar diferencias, calculá los totales con estas reglas:

| Concepto                 | Decimales | Cómo se calcula                                                                                                  |
| ------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------- |
| Precio unitario del ítem | hasta 3   | Lo envías vos.                                                                                                   |
| Subtotal por alícuota    | 2         | Suma de cantidad × precio unitario - bonificacion, de los ítems de esa alícuota, redondeada con Round Half Even. |
| IVA por alícuota         | 2         | Subtotal **sin redondear** × alícuota, redondeado con Round Half Even.                                           |
| Total del comprobante    | 2         | Suma de los subtotales y los impuestos ya redondeados.                                                           |

**Round Half Even** (redondeo bancario) es el método que exige ARCA. Cuando el valor termina exactamente en 5, se redondea al dígito par más cercano:

| Valor  | Redondeado |
| ------ | ---------- |
| 66,165 | 66,16      |
| 66,115 | 66,12      |

***

{% hint style="info" %}
Antes de tomar cualquier decisión, consultá siempre con tu estudio contable para evitar posibles errores y asegurarte de actuar conforme a la normativa vigente.
{% endhint %}

### **Cálculos básicos:**

| Cálculo                   | Fórmula                                                             | Ejemplo                      |
| ------------------------- | ------------------------------------------------------------------- | ---------------------------- |
| **Subtotal del ítem**     | Cantidad × Precio unitario                                          | 2 × $50 = $100               |
| **Bonificación**          | Subtotal del ítem × % de bonificación                               | $100 × 10% = $10             |
| **Precio total del ítem** | Subtotal del ítem − Bonificación                                    | $100 − $10 = $90             |
| **Impuestos internos**    | Precio total del ítem sin IVA × % de impuestos internos             | $90 × 20% = $18              |
| **IVA**                   | Precio total del ítem × % de IVA _(sin incluir impuestos internos)_ | $90 × 21% = $18,90           |
| **Total del ítem**        | Precio total + Impuestos internos + IVA                             | $90 + $18 + $18,90 = $126,90 |

### **¿Cómo se calcula el total de un comprobante?**

El cálculo de validación previa, que garantiza que el total que vos envias coincida con el que la plataforma recalcula, se realiza de la siguiente manera:

{% stepper %}
{% step %}
#### **Paso 1: Subtotal por alícuota**

Sumamos los ítems de cada alícuota de IVA: _cantidad × precio unitario sin IVA − bonificación_. Esta suma **no se redondea**.\
_&#x45;n el PDF, cada ítem se muestra redondeado a 3 decimales._
{% endstep %}

{% step %}
#### **Paso 2: IVA por alícuota**

Calculamos el IVA sobre cada subtotal del paso 1 y lo redondeamos a **2 decimales** (Round Half Even).

> ⚠️ **El IVA no se calcula ítem por ítem.** Se calcula sobre el subtotal de cada alícuota. Si en tu sistema sumás el IVA de cada ítem, pueden aparecer diferencias de centavos.
{% endstep %}

{% step %}
#### **Paso 3: Total del comprobante**

Sumamos los subtotales, los otros impuestos y el IVA, y redondeamos el resultado a **2 decimales** (Round Half Even).
{% endstep %}
{% endstepper %}

### ⚠️ **Tolerancia por redondeo ($0,03) hasta 31/01/2027:**

* **Hoy:** se acepta una diferencia de hasta $0,03.
* **Desde el 14/11/2026:** las cuentas API DEV funcionan sin tolerancia, para que puedas probar tu integración.
* **Desde el 01/02/2027:** no se aceptan diferencias de centavos. Lo que envíes tiene que coincidir exactamente con el recálculo de la plataforma.

### ¿Qué hacer si tengo diferencias con el precio final?

Podes agregar un concepto o ítem denominado **«Ajuste por redondeo»**, con un importe positivo o negativo, según corresponda, y aplicar la **alícuota de IVA que te recomiende tu estudio contable**.

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

