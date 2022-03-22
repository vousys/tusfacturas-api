---
description: >-
  Mediante éste método podrás hacer el reenvío de un comprobante ya emitido a tu
  cliente, siempre y cuando hayas especificado en el cliente, que se le enviaba
  por e-mail.
---

# Reenviar comprobante a un cliente

Tipo de datos: **JSON**\
Charset: **UTF-8**

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/reenviar " method="post" summary="Reenviar un comprobante a tu cliente" %}
{% swagger-description %}
Mediante éste método podrás hacer el reenvío de un comprobante a tu cliente.
{% endswagger-description %}

{% swagger-parameter in="body" name="comprobante" required="false" %}
Un objeto compuesto de los siguientes atributos: ****&#x20;

**tipo:** Campo alfanumérico. Longitud máx: 50 caracteres, conteniendo el tipo de comprobante a consultar. Ej: FACTURA A&#x20;

**operacion :** Campo alfanumérico. Longitud máx: 1 carácter. Valores permitidos (V o C) ya sea para ventas o compras.

**punto\_venta** Campo númerico para indicar el número del punto de venta.

**numero :** Campo numérico. Longitud máx: 8. Indica el número del comprobante a consultar.


{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus Credenciales de acceso.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus Credenciales de acceso.
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de respuesta exitosa el campo " %}
{% tabs %}
{% tab title="JSON" %}
```
{
	"error": "N" 
}
```
{% endtab %}

{% tab title="Plain Text" %}
```
```
{% endtab %}
{% endtabs %}
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON a enviar:

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
