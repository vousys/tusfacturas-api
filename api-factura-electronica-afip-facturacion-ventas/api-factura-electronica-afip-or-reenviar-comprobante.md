---
description: >-
  Mediante éste método podrás hacer el reenvío por e-mail de un comprobante a tu
  cliente las veces que necesites.
---

# Reenviar comprobante a un cliente

Debes tener en cuenta que la función de "reenviar comprobante" solo estará habilitada si al momento de generar el comprobante, habías indicado en el perfil de tu cliente que el comprobante se enviaba por e-mail. &#x20;



## Reenviar un comprobante a tu cliente

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`reenviar`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.



#### Request Body

| Name        | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| comprobante | String | <p>Un objeto compuesto de los siguientes atributos: </p><p><strong>tipo:</strong> Campo alfanumérico. Longitud máx: 50 caracteres, conteniendo el tipo de comprobante a consultar. Ej: FACTURA A </p><p><strong>operacion :</strong> Campo alfanumérico. Longitud máx: 1 carácter. Valores permitidos (V o C) ya sea para ventas o compras.</p><p><strong>punto_venta</strong> Campo númerico para indicar el número del punto de venta.</p><p><strong>numero :</strong> Campo numérico. Longitud máx: 8. Indica el número del comprobante a consultar.</p><p></p> |
| apikey      | string | Tus credenciales de acceso.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| apitoken    | string | Tus Credenciales de acceso.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| usertoken   | string | Tus Credenciales de acceso.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

{% tabs %}
{% tab title="200 En caso de respuesta exitosa el campo " %}
{% tabs %}
{% tab title="JSON" %}
```
{
	"error": "N" 
}
```
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

### Ejemplo del JSON a enviar para reenviar un comprobante:

```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}
```

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
