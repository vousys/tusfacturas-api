---
description: >-
  Consulta desde la API de  TusFacturas.app, la cuenta corriente de tus
  clientes.
---

# Consulta de Cuentas Corrientes

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="v2/clientes/cuenta-corriente" method="post" summary="Consulta de cuenta corriente" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="cliente" type="object" required="false" %}
**documento\_tipo**

**documento\_nro**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" required="false" %}
Tus credenciales de acceso
{% endswagger-parameter %}
{% endswagger %}

### Ejemplo del JSON que debes enviar

```
{
    "usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
    "apikey"    :  "9991",    
    "apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",    
    "cliente":  {       
      "documento_nro":    "30712293841",
      "documento_tipo":   "CUIT"
      }
  }
```

### Estructura de "Cliente"

| `documento_tipo` | <p>Valores Permitidos: <strong>CUIT</strong><br><strong>Ejemplo: CUIT</strong></p>     |
| ---------------- | -------------------------------------------------------------------------------------- |
| `documento_nro`  | <p>Campo numérico, sin puntos ni guiones.<br><strong>Ejemplo: 30111222334</strong></p> |

### Estructura de los datos devueltos

Se devolverá una lista, conteniendo la siguiente estructura, con cada uno de los registros de la cuenta corriente de tu cliente.

```
    {
        "fecha":"11\/05\/2017",
        "concepto":"FACTURA A 0002-00000002 (CUIT DE PRUEBA)",
        "debe":112.1,
        "haber":0,
        "resta_abonar_de_este_comprobante":112.1,
        "saldo":224.2
    }
```
