---
description: >-
  Utilizá la API de facturación electrónica AFIP de TusFacturas.app, para
  eliminar tus comprobantes de compra.
---

# Compras: Eliminación de comprobantes

Tené en cuenta que las compras que cargas en nuestra plataforma no impactan en AFIP y son sólo para tu gestión interna.

{% swagger baseUrl="https://www.tusfacturas.app/app/api/v2/facturacion/comprobante_eliminar" path="" method="post" summary="" %}
{% swagger-description %}
Ten en cuenta que solo podrás eliminar comprobantes de compra si no tienen pagos relacionados. 
{% endswagger-description %}

{% swagger-parameter in="body" name="comprobante" type="object" required="false" %}
Según estructura que se detalla abajo
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus Credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus Credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{"error":"N",
"errores":[],
"rta":"El comprobante se ha eliminado."}
```
{% endswagger-response %}
{% endswagger %}

### Ejemplo de JSON a enviar para eliminar un comprobante:

```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "C",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}
```

### Estructura de "comprobante"

| `tipo`        | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de de compra (C).<br>Valores Permitidos: <strong>C</strong><br><strong>Ejemplo: C</strong></p>                                                  |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero`      | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |

### Ejemplo del JSON de respuesta

```
{"error":"N",
"errores":[],
"rta":"El comprobante se ha eliminado."}
```
