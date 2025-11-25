---
description: >-
  Consulta la información asociada a un CUIT provista en tiempo real desde ARCA
  y obtene los datos en formato JSON.
icon: code
---

# Consultar CUIT en ARCA

{% hint style="info" %}
**IMPORTANTE**: Para utilizar esta consulta, tu CUIT debe estar **enlazado con ARCA**. Por lo tanto, esta funcionalidad **no está disponible** en el plan API DEV.
{% endhint %}

### Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">clientes/afip-info</mark>
{% endhint %}

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

### Ejemplo de JSON para consultar un CUIT en ARCA

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
​
```

### JSON de respuesta exitosa

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

***

### Parámetros para consultar un CUIT en ARCA&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la documentación de la API del método de [consulta de CUIT en ARCA](../consultas-varias-a-servicios-afip-arca/api-factura-electronica-afip-clientes-consultar-cuit-en-constancia-de-inscripcion.md), para obtener información detallada de los posibles errores, datos devueltos y comentarios adicionales

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
