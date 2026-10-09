---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de incoterms  .
---

# Consulta de Incoterms

### Parámetros: Consulta de Incoterms

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/tablas_referencia/`<mark style="color:purple;">**`incoterms`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request =  1 llamada`\
Los requests se cuentan individualmente por cada método utilizado. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

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
