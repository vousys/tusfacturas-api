---
description: >-
  Mediante éste servicio podrás consultar el estado de los servicios de
  facturación AFIP/ARCA, como así también el estado del servicio API.
icon: code
---

# Estado de los servicios

## Consultá el estado de los servicios de TusFacturasAPP y el estado de los servicios de facturación de ARCA

{% hint style="danger" %}
**Los servicios de AFIP/ARCA se caen regularmente.**

Tene en cuenta que todos nuestros métodos controlan internamente el estado de los servicios AFIP/ARCA, y si alguno no se encuentra operativo, automáticamente vas a recibir la respuesta correspondiente en cada request que envíes, junto con su mensaje de error.
{% endhint %}

### Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`estado_servicios/alertas`</mark>
{% endhint %}

### Ejemplo del JSON a enviar para consultar el estado de los servicios

{% code title="JSON" %}
```
{
	"usertoken": "xxxxx",
	"apikey": "xxx",
	"apitoken": "xxxx"
}

```
{% endcode %}

### Response

En caso de no detectarse errores, la variable `error` será devuelta con el valor `"N"`, junto con las variables detalladas a continuación.

La variable `facturacion` devolverá `"OK"` cuando los servicios de ARCA funcionen correctamente. En caso contrario, se informará un mensaje de alerta con el detalle de la incidencia detectada y si estas facturando en la modalidad instantánea, tus requests serán rechazados.

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



### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
