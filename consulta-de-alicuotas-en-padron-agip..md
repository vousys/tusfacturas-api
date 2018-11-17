---
description: API para consultar al padrón AGIP las alícuotas de percepción y retención.
---

# Consulta de alícuotas en padrón AGIP.

{% hint style="info" %}
El CUIT a consultar debe existir previamente en tu base de clientes.
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api/" path="v2/clientes/agip-padron" %}
{% api-method-summary %}
Consulta en padrón ARBA
{% endapi-method-summary %}

{% api-method-description %}
El método te devolverá las alícuotas \(en porcentajes\) que le corresponden según ARBA.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="cliente" required=true type="object" %}
**documento\_tipo** Valores Permitidos: CUIT , DNI Ejemplo: DNI  
**documento\_nro** Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334  
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso.
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso.
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación.
{% endapi-method-response-example-description %}

```text
{
   "error":     "N",
   "errores":  [  "" ],
   "rta":      "OK",
   "alicuota_percepcion": 3,
   "alicuota_retencion":  5,
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Estructura del JSON a enviar

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"cliente":  {                
      "documento_nro":    "30712293841",
      "documento_tipo":   "CUIT"        
           }
 }
```

## Estructura de "Cliente"

| `documento_tipo` | Valores Permitidos: **CUIT**  |
| :--- | :--- |
| `documento_nro` | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |

