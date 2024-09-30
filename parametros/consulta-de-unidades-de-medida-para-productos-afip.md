---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  unidades de medida definidas por AFIP
---

# Consulta de unidades de medida AFIP

### Parámetros: Consulta de Unidades de medida

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`tablas_referencia/unidades_medida`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

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
