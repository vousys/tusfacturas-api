# Eliminación de comprobantes de Compra

{% api-method method="post" host="https://www.tusfacturas.app/app" path="/api/v2/facturacion/comprobante\_eliminar" %}
{% api-method-summary %}
Eliminar comprobante
{% endapi-method-summary %}

{% api-method-description %}
Ten en cuenta que solo podrás eliminar comprobantes de compra si no tienen pagos relacionados.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="comprobante" type="object" required=true %}
Según estructura que se detalla abajo
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus Credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus Credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{"error":"N",
"errores":[],
"rta":"El comprobante se ha eliminado."}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo de JSON a enviar para eliminar un comprobante:

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "C",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}
```

### Estructura de "comprobante"

| `tipo` | Campo numérico según tabla de referencia de [Tipos de comprobantes\(\*\*\*\)](https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes). **Ejemplo: FACTURA B** |
| :--- | :--- |
| `operacion` | Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de de compra \(C\).  Valores Permitidos: **C** **Ejemplo: C** |
| `punto_venta` | Campo numérico entero. Longitud máxima 4 digitos. **Ejemplo: 3** |
| `numero` | Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante. **Ejemplo: 4567** |

