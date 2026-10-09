---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  alícuotas existentes en el padrón AGIP Padrón de Regímenes Generales (Cod. de
  Norma 029)
---

# Consultar las alícuotas en AGIP Padrón de Regímenes Generales

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/clientes/`<mark style="color:purple;">**`agip-padron`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request = 1 llamada`\
Los requests se cuentan individualmente por cada método utilizado. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}



Éste método te devolverá las alícuotas (el valor  porcentual) que le corresponden según AGIP **para el mes en curso.**

#### Request Body

| Name      | Type   | Description                                                                                                                                                                                                                                              |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cliente   | object | <p>Un objeto conteniendo los siguientes datos:</p><p><strong>documento_tipo</strong></p><p>Valores Permitidos: CUIT , DNI Ejemplo: DNI</p><p><strong>documento_nro</strong></p><p>Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334</p><p></p> |
| usertoken | string | Tus credenciales de acceso.                                                                                                                                                                                                                              |
| apitoken  | string | Tus credenciales de acceso.                                                                                                                                                                                                                              |
| apikey    | string | Tus credenciales de acceso                                                                                                                                                                                                                               |

{% hint style="info" %}
CUITS con alícuota cero:

En el supuesto caso que la consulta te retorne alícuota cero, deberás evaluar si corresponde o no, aplicar el porcentaje máximo a retener/percibir.

Previo al 01/01/2019, éste padrón podía ser descargado públicamente desde la web de AGIP, pero ahora se realiza únicamente una consulta individual accediendo con clave ciudad; motivo por el cual, nuestra plataforma no puede retornarte la información exacta.

Ten en cuenta que solo almacenamos la información descargada desde AGIP para el mes actual. No podrás consultar meses anteriores.
{% endhint %}

## Estructura del JSON a enviar

```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxxx",
"cliente":  {                
      "documento_nro":    "30712293841",
      "documento_tipo":   "CUIT"        
           }
 }
```

## Estructura de "Cliente"

| `documento_tipo` | Valores Permitidos: **CUIT**                                    |
| ---------------- | --------------------------------------------------------------- |
| `documento_nro`  | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |
|                  |                                                                 |

{% tabs %}
{% tab title="Respuesta" %}
```
Ejemplo de cuando existe en padron AGIP

{
   "error":     "N",
   "existe_padron":     "S",
   "errores":  [  "" ],
   "rta":      "OK",
   "alicuota_percepcion": 3,
   "alicuota_retencion":  5,
}



Ejemplo de cuando NO existe en padron AGIP

{
   "error":     "N",
   "existe_padron":     "N",
   "errores":  [  "" ],
   "rta":      "OK",
   "alicuota_percepcion": 0,
   "alicuota_retencion":  0,
}



Ejemplo de cuando NO existe en tu base de clientes

{
   "error":     "S",
   "existe_padron":     "-",
   "errores":  [  "El cliente no existe en tu cartera" ],
   "rta":      "OK",
   "alicuota_percepcion": 0,
   "alicuota_retencion":  0,
}




```
{% endtab %}
{% endtabs %}
