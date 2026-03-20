---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de CUIT pais definidos por AFIP
---

# Consulta de CUITs País en AFIP

### Parámetros: Consulta de cuit país

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`tablas_referencia/cuit_pais`</mark>

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
