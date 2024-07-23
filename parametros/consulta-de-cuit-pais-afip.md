---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de CUIT pais definidos por AFIP
---

# Parámetros:  Consulta de los CUIT País en AFIP

## Consulta de cuit país

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`tablas_referencia/cuit_pais`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción



#### Request Body

| Name      | Type   | Description                |
| --------- | ------ | -------------------------- |
| apikey    | string | Tus credenciales de acceso |
| apitoken  | string | Tus credenciales de acceso |
| usertoken | string | Tus credenciales de acceso |

{% tabs %}
{% tab title="200 En caso de no existir errores, se devolverá la variable error con un valor " %}
```
{
        "error":     "N",
        "errores":   [ "" ],
        "items":  [
                        {"id":"51600003015","descripcion":"AFGANISTAN - Otro tipo de Entidad"},
                        {"id":"50000003015","descripcion":"AFGANISTAN - Persona Fisica"}
                  ] 
 }
```
{% endtab %}
{% endtabs %}

### Ejemplo del JSON a enviar

```
{ 
 "usertoken" :  "xxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxxx" 
}
```
