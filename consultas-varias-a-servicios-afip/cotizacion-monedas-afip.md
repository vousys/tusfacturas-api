---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, las
  diferentes cotizaciones de monedas brindadas por AFIP.
---

# Consultar las cotizaciones AFIP

Accede a cotizaciones de monedas AFIP en tiempo real con la API de facturación electrónica de TusFacturas.app

Obtene información precisa y actualizada sobre el tipo de cambio oficial de AFIP para sus facturas electrónicas.

### Beneficios de utilizar la API de facturación electrónica de TusFacturas.app para consultar cotizaciones de monedas AFIP:

* Información en tiempo real: Accedes a las últimas cotizaciones de monedas AFIP al momento de generar sus facturas electrónicas.&#x20;
* Precisión garantizada: Obtenes datos oficiales directamente de AFIP, eliminando la necesidad de realizar cálculos manuales o utilizar fuentes no confiables.&#x20;
* Eficiencia optimizada: Automatizas la consulta de cotizaciones de monedas AFIP, ahorrando tiempo y esfuerzo en su proceso de facturación electrónica.&#x20;
* Integración perfecta: Integra la consulta de cotizaciones de monedas AFIP en tu sistema de gestión existente para una experiencia fluida y automatizada.&#x20;

TusFacturas.app es la solución ideal para empresas que buscan simplificar y optimizar su proceso de facturación electrónica, incluyendo la consulta precisa y automatizada de cotizaciones de monedas AFIP.

Comenza a utilizar la API de facturación electrónica de TusFacturas.app hoy mismo y experimenta la diferencia.

{% hint style="info" %}
Ten en cuenta que para la moneda "dólar": AFIP trabaja con la cotización oficial del Banco de la Nación Argentina, correspondiente al DOLAR DIVISAS y la cotización es actualizada a cada hora.
{% endhint %}

## Request

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`tablas_referencia/cotizacion`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.



Puedes obtener la cotización de las diferentes monedas que tenemos publicadas en nuestra

[**tabla de referencia de monedas**](../parametros/tablas-de-referencia.md#monedas)

#### Request Body

| Name      | Type   | Description                                                                                                                                                                                                                     |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| usertoken | string | Tus credenciales de acceso                                                                                                                                                                                                      |
| apitoken  | string | Tus credenciales de acceso                                                                                                                                                                                                      |
| apikey    | string | Tus credenciales de acceso                                                                                                                                                                                                      |
| moneda    | string | La moneda a consultar, según nuestra [tabla de referencia de monedas](../parametros/tablas-de-referencia.md#monedas). En caso que no envies éste dato, obtendrás la cotización del dolar.                                       |
| fecha     | string | <p>Si indicas la fecha en formato dd/mm/aaaa, te mostraremos la ultima cotización encontrada en AFIP para ese día, según los datos que hemos almacenado. Ten en cuenta que no podrás consultar mas de 2 meses atras.</p><p></p> |

### Estructura del JSON a enviar

{% code title="JSON" %}
```
{
   "usertoken" :  "xxxx",
   "apikey"    :  "xxxx",
   "apitoken"  :  "xxxx",
   "moneda"    :  "012",
   "fecha"     :  "02/03/2020"
 }
```
{% endcode %}

### Ejemplo de un JSON de respuesta exitosa

```
 {
        "error":     "N",
        "errores":
                    [
                        ""
                    ],
        "cotizacion": "15.10"
    }
```
