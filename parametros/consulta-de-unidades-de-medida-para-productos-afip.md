---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  unidades de medida definidas por AFIP
---

# Parámetros: Consulta de unidades de medida AFIP, para productos

## Consulta de Unidades de medida

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`tablas_referencia/unidades_medida`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción

#### Request Body

| Name      | Type   | Description                |
| --------- | ------ | -------------------------- |
| apikey    | string | Tus credenciales de acceso |
| apitoken  | string | Tus credenciales de acceso |
| usertoken | string | Tus credenciales de acceso |

### Ejemplo del JSON a enviar

```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxx"
}
```
