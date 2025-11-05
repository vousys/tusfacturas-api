---
description: >-
  Consulta la información básica de tu cliente, desde la constancia de
  inscripción de AFIP/ARCA, y obtené los datos en formato JSON.
---

# Consultar datos de un CUIT, desde la constancia de inscripción

{% hint style="info" %}
**IMPORTANTE**: Para utilizar esta consulta, tu CUIT debe estar **enlazado con ARCA**. Por lo tanto, esta funcionalidad **no está disponible** en el plan API DEV.
{% endhint %}

## Consultar datos de un CUIT en AFIP/ARCA

Mediante éste método podrás consultar la info que AFIP/ARCA tiene almacenada en su base de datos con relación a un CUIT. Ésta info es lo mismo que visualizas cuando haces una [consulta web a la constancia de inscripción](https://seti.afip.gob.ar/padron-puc-constancia-internet/ConsultaConstanciaAction.do).  Tene en cuenta que la información provista en éste método no tiene relación con la info de tus clientes que tengas almacenados en TusFacturasAPP.

#### ¿A donde enviar el request?

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`clientes/afip-info`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

| Name      | Type   | Description                 |
| --------- | ------ | --------------------------- |
| cliente   | string | Objeto de tipo cliente      |
| apikey    | string | Tus credenciales de acceso  |
| usertoken | string | Tus credenciales de acceso. |
| apitoken  | string | Tus credenciales de acceso. |

{% tabs %}
{% tab title="¿Qué te retorna la llamada? " %}
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
   "apoc_existe": "SI",
    "apoc_info": "CUIT en base APOC desde el 22/07/2019.  (base APOC actualizada al 26/08/2024 18:42) -  Sugerimos consultar con su estudio contable inmediatamente.",
   "errores":  [  "" ] 
}
​
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Ejemplo del JSON a enviar <a href="#estructura-del-json-a-enviar" id="estructura-del-json-a-enviar"></a>

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

### Estructura del bloque "Cliente" <a href="#estructura-de-cliente" id="estructura-de-cliente"></a>

| `documento_tipo` | Valores Permitidos: **CUIT**                                    |
| ---------------- | --------------------------------------------------------------- |
| `documento_nro`  | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |

#### Ejemplo del JSON de respuesta exitosa

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
   "apoc_existe": "SI",
   "apoc_info": "CUIT en base APOC desde el 22/07/2019.  (base APOC actualizada al 26/08/2025 18:42) -  Sugerimos consultar con su estudio contable inmediatamente.",
   "errores":  [  "" ] 
}
```

#### Ejemplo de respuesta cuando ARCA  bloquea la constancia de inscripción:

```
{
	"error": "S",
	"errores": [
		[
			"El servicio de consulta de CUIT en AFIP retorna el siguiente error:   - La CUIT registra pendiente la constitución del domicilio fiscal electrónico de acuerdo a lo normado en la RG 4280/18 AFIP.,La CUIT registra una o más actividades económicas que no pertenecen al nomenclador de actividades vigente F. 883 RG AFIP3587/13."
		]
	]
}
```

#### Ejemplo de respuesta, cuando el CUIT no tiene impuestos asociados en ARCA y no se puede determinar su condición fiscal

```
{
	"error": "S",
	"errores": [
		"No se ha podido recuperar la condicion frente al IVA de este CUIT"
	],
	"razon_social": "CONSORCIO DE COPROPIETARIOS XXX",
	"condicion_impositiva": "CONSUMIDOR FINAL",
	"direccion": "XXXX 179",
	"localidad": "LOMAS DE ZAMORA",
	"codigopostal": "CP: 1832",
	"provincia": "BUENOS AIRES",
	"estado": "ACTIVO",
	"actividad": [
		{
			"descripcion": "SERVICIOS DE CONSORCIOS DE EDIFICIOS",
			"id": 949920,
			"nomenclador": 883,
			"periodo": 201311
		}
	],
	"apoc_existe": "NO",
	"apoc_info": ""
}
```

#### "condicion\_impositiva": Posibles valores de la respuesta obtenida desde AFIP/ARCA.

condicion\_impositiva puede retornar alguno de los siguientes valores:

* MONOTRIBUTO
* EXENTO
* RESPONSABLE INSCRIPTO

{% hint style="info" %}
Ten en cuenta que:

1. &#x20;Si el CUIT no se encuentra inscripto en ningún impuesto, nuestra plataforma te devolverá los datos que ésta encuentra en AFIP,  pero el campo "error"  en "S", ya que no podemos determinar que la condición frente al IVA.
2. Si el CUIT que estas consultando tiene requerimientos pendientes por responder o alguna otra inconsistencia en AFIP, el propio organismo bloquea el acceso a la información de su constancia y recibirás un error.
{% endhint %}
