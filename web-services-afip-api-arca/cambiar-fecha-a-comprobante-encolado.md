---
description: >-
  Utiliza la API de TusFacturasAPP, para cambiar la fecha de aquellos
  comprobantes que se encuentran en cola de procesamiento
icon: code
---

# Cambiar fecha a comprobante encolado

Este método permite **cambiar la fecha de un comprobante** que se encuentra en la cola de procesamiento.

**Consideraciones importantes:**

* La fecha asignada al comprobante determinará su **fecha de emisión**.
* El sistema solo procesa y emite de la cola aquellos comprobantes cuya fecha sea **igual o anterior a la fecha actual**.

### &#x20;Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`cambiar_fecha_encolado`</mark>
{% endhint %}

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

### Ejemplo del JSON a enviar:

```
{
    "apitoken":"xxxx",
    "apikey": "xxx",
    "usertoken":"xxxx",
    "external_reference": "mi_ext_rf" ,
    "fecha": "25/03/2022",
    "vencimiento": "28/03/2022"
	 
}
 
```

#### Estructura del Body

| Name                | Type   | Description                                                                      |
| ------------------- | ------ | -------------------------------------------------------------------------------- |
| apikey              | string | Tus credenciales de acceso.                                                      |
| apitoken            | string | Tus Credenciales de acceso.                                                      |
| usertoken           | string | Tus Credenciales de acceso.                                                      |
| fecha               | string | Fecha del comprobante. Formato esperado: dd/mm/aaaa                              |
| external\_reference | String | Campo alfanumérico de hasta 255 caracteres.                                      |
| vencimiento         | String | Fecha de vencimiento del pago de dicho comprobante. Formato esperado: dd/mm/aaaa |

### 📌 Respuestas posibles

Si, excepcionalmente, una `external_reference` se asocia a más de un comprobante, el sistema tomará la información del **primer comprobante encontrado**.

#### ✅ Response exitoso:

Al enviar la petición, recibirás instantáneamente la siguiente respuesta:

```
{
	"error": "N",
	"errores": []
}
```

y también recibirás un webhook, para informarte de dicha eliminación:

```
{
	"creado": "18/03/2022 15:58:11",
	"evento": "cambio_fecha",
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

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
