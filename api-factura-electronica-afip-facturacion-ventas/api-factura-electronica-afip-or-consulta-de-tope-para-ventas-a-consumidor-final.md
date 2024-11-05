---
description: >-
  Consulta fácil y rápido el tope AFIP/ARCA para ventas a consumidor final. ¡Sin
  necesidad de datos del comprador!
---

# Consultar el tope para ventas a consumidor final

Conocé toda la info que debes enviar para poder generar [facturas B](api-factura-electronica-afip-factura-nota-de-debito-b-nota-de-credito-bb.md) o [Facturas C](api-factura-electronica-afip-factura-c-nota-de-debito-c-nota-de-credito-c.md)  [a consumidor final sin especificar los datos del comprador](facturas-a-consumidor-final-sin-especificar-datos.md).



### Método para consulta de tope a ventas a consumidor final provisto por AFIP/ARCA

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`topecf`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

| Name      | Type   | Description                |
| --------- | ------ | -------------------------- |
| apikey    | String | Tus credenciales de acceso |
| apitoken  | String | Tus credenciales de acceso |
| usertoken | String | Tus credenciales de acceso |



{% tabs %}
{% tab title="200: OK " %}
```javascript
{
	"error": "N",
	"errores": [],
	"monto": 26228
}
```
{% endtab %}
{% endtabs %}

### Ejemplo de JSON a enviar

```
{
    "apitoken":"xxxx",
    "apikey": xxx,
    "usertoken":"xxxx"
}
```



TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
