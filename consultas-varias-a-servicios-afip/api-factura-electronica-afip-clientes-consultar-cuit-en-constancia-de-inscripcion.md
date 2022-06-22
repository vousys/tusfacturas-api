---
description: >-
  Consulta la información básica de tu cliente, desde la constancia de
  inscripción de AFIP, y obtené los datos en formato JSON.
---

# Consultar datos de un CUIT, desde la constancia de inscripción

{% hint style="info" %}
El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso.

**IMPORTANTE**: Para poder realizar ésta consulta, deberás tener agregado en tu cuenta AFIP, el servicio de CONSULTA DE CONSTANCIA DE INSCRIPCIÓN. Te indicamos como hacerlo en el[ instructivo de integración con AFIP : Paso 5](https://www.tusfacturas.app/app/afip-como-enlazar-con-tusfacturas.html)
{% endhint %}

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="/v2/clientes/afip-info" method="post" summary="Obtener datos de un CUIT" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="cliente" type="string" required="false" %}
Objeto de tipo cliente
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
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

## Ejemplo del JSON a enviar <a href="#estructura-del-json-a-enviar" id="estructura-del-json-a-enviar"></a>

{% code title="JSON" %}
```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxx",
"cliente":  {                      
    "documento_nro":    "30712293841",      
    "documento_tipo":   "CUIT"                   
    } 
 }
```
{% endcode %}

### Estructura de "Cliente" <a href="#estructura-de-cliente" id="estructura-de-cliente"></a>

| `documento_tipo` | Valores Permitidos: **CUIT**                                    |
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

### Posibles valores, de la respuesta obtenida.

condicion\_impositiva puede retornar los siguientes valores:

* MONOTRIBUTO
* EXENTO
* RESPONSABLE INSCRIPTO

{% hint style="info" %}
Ten en cuenta que:

1. &#x20;Si el CUIT no se encuentra inscripto en ningún impuesto, nuestra plataforma te devolverá los datos que ésta encuentra en AFIP,  pero el campo "error"  en "S", ya que no podemos determinar que la condición frente al IVA.
2. Si el CUIT que estas consultando tiene requerimientos pendientes por responder o alguna otra inconsistencia en AFIP, el propio organismo bloquea el acceso a la información de su constancia y recibirás un error.
{% endhint %}
