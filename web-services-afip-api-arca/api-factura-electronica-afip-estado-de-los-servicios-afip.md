---
description: >-
  Mediante éste servicio podrás consultar el estado de los servicios de
  facturación AFIP/ARCA, como así también el estado del servicio API.
icon: person-digging
---

# Estado de los servicios y Tareas de mantenimientos programados

## Consulta el estado de los servicios en TusFacturasAPP y el estado de los servicios de ARCA

{% hint style="danger" %}
**Los servicios de ARCA (ex AFIP) se caen regularmente.**

Ante una caída, la **facturación instantánea (sincrónica) se ve afectada de inmediato**: recibirás un error en cada request que intente impactar en ARCA. La **facturación asincrónica puede seguir funcionando**, ya que los comprobantes se encolan y se procesan cuando el servicio se restablece. Todos nuestros métodos controlan internamente el estado de los servicios de ARCA y te devuelven la respuesta correspondiente con su mensaje de error.
{% endhint %}

### Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`estado_servicios/alertas`</mark>
{% endhint %}

### Ejemplo del JSON a enviar para consultar el estado de los servicios

{% code title="JSON" %}
```json
{
	"usertoken": "xxxxx",
	"apikey": "xxx",
	"apitoken": "xxxx"
}

```
{% endcode %}

### Response

En caso de no detectarse errores, la variable `error` será devuelta con el valor `"N"`, junto con las variables detalladas a continuación.

La variable `facturacion` devolverá `"OK"` cuando los servicios de ARCA funcionen correctamente. En caso contrario, se informará un mensaje de alerta con el detalle de la incidencia detectada. Si facturas en **modalidad instantánea (sincrónica)**, tus requests serán rechazados de inmediato. Si usas **facturación asincrónica**, los comprobantes podrán seguir encolándose y procesarse una vez que ARCA restablezca el servicio.

Dentro del bloque `prox_mantenimientos_programados` te informaremos las próximas tareas de mantenimiento programadas, ya sea por nuestro equipo o por ARCA.

Cuando las tareas sean realizadas por nuestro equipo, durante ese período no podrás acceder a la plataforma y todas las solicitudes enviadas vía API serán rechazadas hasta la finalización de las mejoras implementadas.

En el caso de mantenimientos programados por ARCA, únicamente serán rechazados los requests que impacten en la facturación instantánea.

Ten en cuenta que también podrán realizarse tareas de mantenimiento de urgencia que, debido a la inmediatez con la que deban aplicarse, podrían no encontrarse previamente listadas dentro de este bloque.

```json
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
	"facturacion": "OK",
	"prox_mantenimientos_programados": [
		{
			"desde": "30/05/2026 08:29",
			"hasta": "30/05/2026 11:29",
			"titulo": "Mantenimiento programado",
			"texto": "Te informamos que realizaremos tareas de mantenimiento en nuestra plataforma entre las XX y las XX. Durante este tiempo, no podras acceder a la plataforma hasta que finalicen las mejoras implementadas."
		}
	],
	"novedades": "24\/03\/2016 | App M\u00f3vil - Actualizaci\u00f3nYa se encuentra disponible para Iphone\/Ipad , la version 2.1 de nuestra app m\u00f3vil.  Descargala! 17\/03\/2016 | Reclamo de deudas autom\u00e1tico: Ahora podes indicar la cantidad de dias desde cuando el sistema empieza a reclamarle a tu cliente la deuda. Ingres\u00e1 a cliente y configuralo ",
}
```

### Mantenimientos programados

En ocasiones, nuestro equipo técnico realiza tareas de mantenimiento programado que requieren suspender temporalmente la operatoria de la API o bien ARCA programa tareas de mantenimiento sobre sus servicios de facturación. Durante ese período, las solicitudes devolverán una respuesta JSON como la siguiente:

```json
{
	"error": "S",
	"mantenimiento": 1,
	"mantenimiento_hasta": "26/07/2026 05:25",
	"errores": [
		"Estaremos realizando tareas de mantenimiento hasta las 05:25"
	]
}
```

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
