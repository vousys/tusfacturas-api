---
description: >-
  Utilizá la API de facturación electrónica de TusFacturas.app, para eliminar
  tus comprobantes de compra.
---

# API Factura electrónica AFIP  - Compras: Eliminación de comprobantes

{% swagger baseUrl="https://www.tusfacturas.app/app" path="/api/v2/facturacion/comprobante_eliminar" method="post" summary="Eliminar comprobante" %}
{% swagger-description %}
Ten en cuenta que solo podrás eliminar comprobantes de compra si no tienen pagos relacionados.
{% endswagger-description %}

{% swagger-parameter in="body" name="comprobante" type="object" %}
Según estructura que se detalla abajo
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus Credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
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
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
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
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de de compra (C). <br>Valores Permitidos: <strong>C</strong><br><strong>Ejemplo: C</strong></p>                                                 |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero`      | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |
