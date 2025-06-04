---
description: >-
  Utiliza la API de TusFacturasAPP, para re-enviar a procesar aquellos
  comprobantes que se encuentran en cola de procesamiento con error
icon: code
---

# Reenvío de Comprobantes Encolados con Error

Esta funcionalidad permite reenviar un comprobante que se encuentra en la cola de procesamiento con un estado de error. Es útil para errores de tipo transitorio o de comunicación.

**Consideración Crítica:** Si el error reportado es una inconsistencia o falta de datos, el reprocesamiento no tendrá efecto. En tal escenario, se recomienda **eliminar el comprobante original** y enviar una **nueva solicitud con los datos corregidos**.

### Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`reenviar_encolado`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.
{% endhint %}

### Ejemplo del JSON a enviar:

```
{
    "apitoken":"xxxx",
    "apikey": "xxx",
    "usertoken":"xxxx",
    "external_reference": "mi_ext_rf"  
}
 
```

### 📌 Respuestas posibles

Ante la existencia de más de un comprobante para una misma `external_reference`, se priorizará el **primer comprobante detectado** por el sistema.

#### ✅ Response exitoso

Al enviar la petición, recibirás instantáneamente la siguiente respuesta:

```
{
	"error": "N",
	"errores": []
}
```

y también recibirás un webhook, para informarte que el comprobante se ha enviado a la cola de procesamiento:

```
{
	"creado": "18/03/2022 15:58:11",
	"evento": "encolado",
	"recurso": "facturacion",
	"external_reference": "mi_extref",
	"intento": 1,
	"msg": [],
	"hook_id": "xxxxx"
}
```

#### 🛑 Response con error

```
{
	"error": "S",
	"errores": [
		"No se han encontrado comprobantes."
	]
}
```

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
