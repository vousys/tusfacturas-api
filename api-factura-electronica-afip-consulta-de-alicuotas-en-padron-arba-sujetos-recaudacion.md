---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  alícuotas existentes en el padrón ARBA sujetos recaudación
---

# API Factura electrónica AFIP  - Consulta de alícuotas en padrón ARBA sujetos recaudación

{% hint style="info" %}
El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso. 

Siempre es importante que re-confirmes con tus asesores impositivos si la alícuota obtenida corresponde o no ser aplicada al comprobante que vas a emitir.
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/clientes/arba-padron" method="post" summary="Consulta en padrón ARBA" %}
{% swagger-description %}
El método te devolverá las alícuotas (en porcentajes) que le corresponden según ARBA.
{% endswagger-description %}

{% swagger-parameter in="body" name="cliente" type="object" %}
**documento_tipo**

    Valores Permitidos: CUIT , DNI Ejemplo: DNI 

\




**documento_nro**

    Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación.

" %}
{% code title="JSON" %}
```

Ejemplo de cuando existe en padron 
​
{
   "error":     "N",
   "existe_padron":     "S",
   "errores":  [  "" ],
   "rta":      "OK",
   "alicuota_percepcion": 3,
   "alicuota_retencion":  5,
}
​
​
​
Ejemplo de cuando NO existe en padron 
​
{
   "error":     "N",
   "existe_padron":     "N",
   "errores":  [  "" ],
   "rta":      "OK",
   "alicuota_percepcion": 0,
   "alicuota_retencion":  0,
}
​
​
​
Ejemplo de cuando NO existe en tu base de clientes
​
{
   "error":     "S",
   "existe_padron":     "-",
   "errores":  [  "El cliente no existe en tu cartera" ],
   "rta":      "OK",
   "alicuota_percepcion": 0,
   "alicuota_retencion":  0,
}

```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
CUITS con alícuota cero:

En el supuesto caso que la consulta te retorne alícuota cero, deberás evaluar con tu contador/a si corresponde o no, aplicar el porcentaje máximo a retener/percibir 
{% endhint %}

### Estructura del JSON a enviar 

```
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

### Estructura de "Cliente"

| `documento_tipo` | <p>Valores Permitidos: <strong>CUIT , DNI</strong><br><strong>Ejemplo: DNI</strong></p> |
| ---------------- | --------------------------------------------------------------------------------------- |
| `documento_nro`  | <p>Campo numérico, sin puntos ni guiones.<br><strong>Ejemplo: 30111222334</strong></p>  |
