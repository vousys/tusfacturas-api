---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app,  toda la
  información básica relacionada con un CUIT. Los datos obtenidos son los que
  observas en la constancia de inscripción.
---

# API Factura electrónica AFIP - Clientes: Consultar CUIT en constancia de inscripción

{% hint style="info" %}
El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso.

IMPORTANTE: Para poder realizar ésta consulta,  deberás tener agregado en tu cuenta AFIP, el servicio de CONSULTA DE CONSTANCIA DE INSCRIPCIÓN. Te indicamos como hacerlo en el[ instructivo de integración con AFIP : Paso 5  ](https://www.tusfacturas.app/app/afip-como-enlazar-con-tusfacturas.html)
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/clientes/afip-info" method="post" summary="Obtener datos de un CUIT" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="cliente" type="string" %}
Objeto de tipo cliente
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
{% code title="JSON" %}
```
{
   "error":             "N",
   "razon_social":      "LA RAZON SOCIAL O NOMBRE",
   "condicion_impositiva": "RESPONSABLE INSCRIPTO",
   "direccion": "la calle 123",
   "localidad": "Castelar",
   "codigopostal": "1712",
   "estado":"ACTIVO",
   "provincia": "BUENOS AIRES",
   "actividad":[
        {
            "descripcion":"SERVICIOS DE CONSULTORES EN INFORM\u00c3\u0081TICA Y SUMINISTROS DE PROGRAMAS DE INFORM\u00c3\u0081TICA",
            "id":"620100",
            "nomenclador":"883",
            "periodo":"201311"
         },
         {
            "descripcion":"SERVICIOS EMPRESARIALES N.C.P.",
            "id":"829900",
            "nomenclador":"883",
            "periodo":"201906"
         }
   ],
   "errores":  [  "" ] 
}
​

```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

## Ejemplo del JSON a enviar <a href="estructura-del-json-a-enviar" id="estructura-del-json-a-enviar"></a>

{% code title="JSON" %}
```
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"cliente":  {                      
    "documento_nro":    "30712293841",      
    "documento_tipo":   "CUIT"                   
    } 
 }

```
{% endcode %}

### Estructura de "Cliente" <a href="estructura-de-cliente" id="estructura-de-cliente"></a>

| `documento_tipo` | Valores Permitidos: **CUIT  **                                  |
| ---------------- | --------------------------------------------------------------- |
| `documento_nro`  | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |



### Ejemplo del JSON de respuesta

```
{
   "error":             "N",
   "razon_social":      "LA RAZON SOCIAL O NOMBRE",
   "condicion_impositiva": "RESPONSABLE INSCRIPTO",
   "direccion": "la calle 123",
   "localidad": "Castelar",
   "codigopostal": "1712",
   "estado":"ACTIVO",
   "provincia": "BUENOS AIRES",
   "actividad":[
        {
            "descripcion":"SERVICIOS DE CONSULTORES EN INFORM\u00c3\u0081TICA Y SUMINISTROS DE PROGRAMAS DE INFORM\u00c3\u0081TICA",
            "id":"620100",
            "nomenclador":"883",
            "periodo":"201311"
         },
         {
            "descripcion":"SERVICIOS EMPRESARIALES N.C.P.",
            "id":"829900",
            "nomenclador":"883",
            "periodo":"201906"
         }
   ],
   "errores":  [  "" ] 
}

```



### Valores posibles de la respuesta obtenida

condicion\_impositiva puede retornar los siguientes valores:

* MONOTRIBUTO
* EXENTO
* RESPONSABLE INSCRIPTO

&#x20;
