---
description: >-
  Mediante éste método podrás hacer el reenvío de un comprobante ya emitido a tu
  cliente, siempre y cuando hayas especificado en el cliente, que se le enviaba
  por e-mail.
---

# API Factura electrónica AFIP | Reenviar comprobante

Tipo de datos: **JSON**\
Charset: **UTF-8**

{% swagger baseUrl="https://www.tusfacturas.app/app/api/" path="v2/facturacion/reenviar " method="post" summary="Reenviar un comprobante a tu cliente" %}
{% swagger-description %}
Mediante éste método podrás hacer el reenvío de un comprobante a tu cliente.
{% endswagger-description %}

{% swagger-parameter in="body" name="comprobante" required="true" %}
**tipo:**

    Campo numérico según tabla de referencia de Tipos de comprobantes(***). Ejemplo: FACTURA B 

\




**operacion:**

    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V  Ejemplo: V 

\




**punto_venta:**

    Campo numérico entero. Longitud máxima 4 dígitos. Ejemplo: 3 

\




**numero:**

    Campo numérico entero. Longitud máxima 8 digitos. Ejemplo: 4567 

\



{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="true" %}
Tus credenciales de acceso.  
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="true" %}
Tus Credenciales de acceso.  
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="true" %}
Tus Credenciales de acceso.
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de respuesta exitosa el campo "error" retornará una "S" y en caso de error una "N" y dentro de errores, una lista con cada uno de los errores encontrados.La estructura de los datos devueltos es igual a la envidada para la generación de los comprobantes.A continuación se visualiza un ejemplo del JSON retornado para el comprobante consultado.Importante: -  Los campos numéricos son retornados como número, salvo el CAE y el CUIT-  Para comprobantes tipo B, el precio ya incluye la alícuota de IVA calculada." %}
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
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}
```
