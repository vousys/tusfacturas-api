---
description: >-
  Consulta fácil y rápido el tope AFIP/ARCA para ventas a consumidor final. ¡Sin
  necesidad de datos del comprador!
icon: code
---

# Consultar el Tope AFIP/ARCA para Ventas a Consumidor Final

Accedé de forma **rápida y sencilla** al monto límite establecido por AFIP/ARCA para tus ventas a consumidor final, ¡sin necesidad de los datos del comprador! Esta herramienta te proporciona la información necesaria para emitir Facturas B o Facturas C a consumidor final sin especificar los datos del cliente, agilizando tu proceso de facturación.

### Endpoint

{% hint style="success" icon="rectangle-api" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`topecf`</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request = 1 llamada`\
Los requests se cuentan independientes por cada método que consumas. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

### Ejemplo de JSON a enviar

```
{
    "apitoken":"xxxx",
    "apikey": xxx,
    "usertoken":"xxxx"
}
```

### JSON de respuesta

```
{
	"error": "N",
	"errores": [],
	"monto": 26228
}
```

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
