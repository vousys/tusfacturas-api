---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  alícuotas existentes en el padrón ARBA sujetos recaudación
---

# Consultar las alícuotas, en el padrón ARBA sujetos recaudación

## Consulta en padrón ARBA

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`clientes/arba-padron`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

El método te devolverá las alícuotas (en porcentajes) que le corresponden según ARBA **para el mes en curso.**

#### Request Body

| Name      | Type   | Description                                                                                                                                                                                                                                       |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cliente   | object | <p>Un objeto conteniendo los siguientes datos:</p><p><strong>documento_tipo</strong></p><p>Valores Permitidos: CUIT , DNI Ejemplo: DNI</p><p><strong>documento_nro</strong></p><p>Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334</p> |
| usertoken | string | Tus credenciales de acceso.                                                                                                                                                                                                                       |
| apitoken  | string | Tus credenciales de acceso.                                                                                                                                                                                                                       |
| apikey    | string | Tus credenciales de acceso                                                                                                                                                                                                                        |

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
