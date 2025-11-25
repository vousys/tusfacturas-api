---
description: Consulta fácil y rápido la cotización oficial del dólar provisto por ARCA.
icon: code
---

# Consultar cotización dolar ARCA

Obtene información en tiempo real y precisa sobre el tipo de cambio oficial de ARCA para sus facturas electrónicas.

Tene en cuenta que para la moneda "dólar", ARCA trabaja con la cotización oficial del Banco de la Nación Argentina, correspondiente al DOLAR DIVISAS y la cotización es actualizada a cada hora.

### Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">tablas\_referencia/cotizacion</mark>
{% endhint %}

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

### Ejemplo de JSON a enviar

```
{
   "usertoken" :  "xxxx",
   "apikey"    :  "xxxx",
   "apitoken"  :  "xxxx",
   "moneda"    :  "DOL",
   "fecha"     :  "02/03/2025"
 }
```

### JSON de respuesta

```
{
        "error":     "N",
        "errores":
                    [
                        ""
                    ],
        "cotizacion": "1500.10"
    }
```

***

### Parámetros para consultar la cotización del dolar en ARCA&#x20;

[TusFacturasAPP](https://www.tusfacturas.app) es un robusto software de facturación respaldado por un estudio contable impositivo que lo mantiene actualizado día a día con los constantes cambios en materia impositivas de Argentina. Consulta la [documentación de la API de facturación AFIP/ARCA](../consultas-varias-a-servicios-afip-arca/cotizacion-monedas-afip.md).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
