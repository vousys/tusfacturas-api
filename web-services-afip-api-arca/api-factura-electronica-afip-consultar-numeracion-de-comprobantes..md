---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la
  numeración de tus comprobantes.
icon: code
---

# Consultar numeración de comprobantes.

### 🧾 ¿Para que sirve la consulta de numeración?

Utiliza este endpoint para obtener el **último número de comprobante emitido** por cada tipo (por ejemplo, Factura E, Nota de Débito A, Factura C) registrado en TusFacturasAPP. Esta funcionalidad es clave para desarrolladores e integradores que necesitan:

* Sincronizar sistemas externos con la numeración oficial de AFIP.
* Asegurar que las nuevas emisiones sigan la secuencia correcta.
* Prevenir errores de duplicidad al generar comprobantes.

### Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/numeracion`
{% endhint %}

💡 El uso de éste método no contabiliza como un request en tu suscripción

### Ejemplo del JSON a enviar

{% code title="JSON" %}
```json
{
	"usertoken": "xxxxx",
	"apikey": "xxxxx",
	"apitoken": "xxxxx",
	"comprobante": {
		"tipo": "NOTA DE DEBITO B",
		"operacion": "V",
		"punto_venta": "2"
	}
}
```
{% endcode %}

#### Estructura del JSON

| `tipo`        | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |

### Ejemplo de JSON de respuesta

```json
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
	"comprobante": {
		"tipo": "NOTA DE DEBITO B",
		"operacion": "V",
		"punto_venta": 2,
		"numero": 6
	}
}
```

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
