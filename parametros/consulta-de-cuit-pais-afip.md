---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de CUIT pais definidos por AFIP
---

# Consulta de CUITs País en AFIP

### Parámetros: Consulta de cuit país

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/tablas_referencia/`<mark style="color:purple;">**`cuit_pais`**</mark>
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

Podes encontrar la lista completa en éste documento, desde la web de ARCA:

[https://www.afip.gob.ar/inversiones-bienes-uso/documentos/CUIT-pais.pdf](https://www.afip.gob.ar/inversiones-bienes-uso/documentos/CUIT-pais.pdf)
