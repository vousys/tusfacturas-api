---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  alícuotas existentes en el padrón ARBA sujetos recaudación
---

# Consultar las alícuotas, en el padrón ARBA sujetos recaudación

{% hint style="info" %}
El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso.

Siempre es importante que re-confirmes con tus asesores impositivos si la alícuota obtenida corresponde o no ser aplicada al comprobante que vas a emitir.
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/clientes/arba-padron" method="post" summary="Consulta en padrón ARBA" %}
{% swagger-description %}
El método te devolverá las alícuotas (en porcentajes) que le corresponden según ARBA.
{% endswagger-description %}

{% swagger-parameter in="body" name="cliente" type="object" required="false" %}
Un objeto conteniendo los siguientes datos:

**documento\_tipo**

Valores Permitidos: CUIT , DNI Ejemplo: DNI

**documento\_nro**

Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}
{% endswagger %}

{% hint style="info" %}
CUITS con alícuota cero:

En el supuesto caso que la consulta te retorne alícuota cero, deberás evaluar con tu contador/a si corresponde o no, aplicar el porcentaje máximo a retener/percibir
{% endhint %}

### Estructura del JSON a enviar

```
{
"usertoken" :  "xxxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxxx",
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

### Ejemplo de respuesta: Cuando se encuentra información en el padrón

```
{
   "error":     "N",
   "existe_padron":     "S",
   "errores":  [  "" ],
   "rta":      "OK",
   "alicuota_percepcion": 3,
   "alicuota_retencion":  5,
}
```

### Ejemplo de respuesta: Cuando no existen datos en el padrón

```
{
   "error":     "N",
   "existe_padron":     "N",
   "errores":  [  "" ],
   "rta":      "OK",
   "alicuota_percepcion": 0,
   "alicuota_retencion":  0,
}
```

### Ejemplo de respuesta: Cuando el cliente no existe en tu base de clientes.

```
{
   "error":     "S",
   "existe_padron":     "-",
   "errores":  [  "El cliente no existe en tu cartera" ],
   "rta":      "OK",
   "alicuota_percepcion": 0,
   "alicuota_retencion":  0,
}
```