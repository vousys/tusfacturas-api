---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  alícuotas existentes en el padrón AGIP Padrón de Regímenes Generales (Código
  de Norma 029)
---

# Consultar las alícuotas, en padrón AGIP

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`clientes/agip-padron`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.



El método te devolverá las alícuotas (en porcentaj) que le corresponden según AGIP.

#### Request Body

| Name      | Type   | Description                                                                                                                                                                                                                                              |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cliente   | object | <p>Un objeto conteniendo los siguientes datos:</p><p><strong>documento_tipo</strong></p><p>Valores Permitidos: CUIT , DNI Ejemplo: DNI</p><p><strong>documento_nro</strong></p><p>Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334</p><p></p> |
| usertoken | string | Tus credenciales de acceso.                                                                                                                                                                                                                              |
| apitoken  | string | Tus credenciales de acceso.                                                                                                                                                                                                                              |
| apikey    | string | Tus credenciales de acceso                                                                                                                                                                                                                               |

{% tabs %}
{% tab title="200 En caso de no existir errores, se devolverá la variable error con un valor " %}
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
