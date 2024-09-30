---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de incoterms  .
---

# Consulta de Incoterms

### Parámetros: Consulta de Incoterms

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`tablas_referencia/incoterms`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

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
    "errores":   
                 [  ""   ],    
     "items":       
              [ 
                       {"id":"EXW","descripcion":"EXW - Vigente del 20100101 a hoy"},
                       {"id":"FCA","descripcion":"FCA - Vigente del 20100101 a hoy"}

              ]
}
```
{% endtab %}
{% endtabs %}

### Ejemplo de JSON a enviar

```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxx"
}
```
