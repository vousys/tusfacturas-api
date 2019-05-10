---
description: >-
  Mediante éste método podrás obtener toda la información básica relacionada con
  un CUIT. Los datos obtenidos son los que observas en la constancia de
  inscripción.
---

# Clientes - Consultar CUIT en constancia de inscripción

{% hint style="info" %}
El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso.

IMPORTANTE: Para poder realizar ésta consulta,  deberás tener agregado en tu cuenta AFIP, el servicio de CONSULTA DE CONSTANCIA DE INSCRIPCIÓN. Te indicamos como hacerlo en el[ instructivo de integración con AFIP : Paso 5  ](https://www.tusfacturas.app/app/afip-como-enlazar-con-tusfacturas.html)
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api" path="/v2/clientes/afip-info" %}
{% api-method-summary %}
Obtener datos de un CUIT
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="cliente" type="string" required=true %}
Objeto de tipo cliente
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso.
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```
{
   "error":             "N",
   "razon_social":      "LA RAZON SOCIAL O NOMBRE",
   "condicion_impositiva": "RESPONSABLE INSCRIPTO",
   "direccion": "la calle 123",
   "localidad": "Castelar",
   "codigopostal": "1712",
   "estado":"ACTIVO",
   "provincia": "BUENOS AIRES"
   "errores":  [  "" ] 
}
​

```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Ejemplo del JSON a enviar <a id="estructura-del-json-a-enviar"></a>

{% code-tabs %}
{% code-tabs-item title="JSON" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}

### Estructura de "Cliente" <a id="estructura-de-cliente"></a>

| `documento_tipo` | Valores Permitidos: **CUIT**   |
| :--- | :--- |
| `documento_nro` | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |

### Valores posibles de la respuesta obtenida

condicion\_impositiva puede retornar los siguientes valores:

* MONOTRIBUTO
* EXENTO
* RESPONSABLE INSCRIPTO

 

