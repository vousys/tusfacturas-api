---
description: >-
  Consulta desde la API de  TusFacturas.app, la cuenta corriente de tus
  clientes.
---

# API TusFacturas.app  - Clientes | Cuenta Corriente

{% swagger baseUrl="https://www.tusfacturas.app/app/api" path="v2/clientes/cuenta-corriente" method="post" summary="Consulta de cuenta corriente" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="cliente" type="object" %}
**documento_tipo**

    Valores Permitidos: CUIT 

\




**documento_nro**

    Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334
{% endswagger-parameter %}

{% swagger-parameter in="body" name="usertoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-parameter in="body" name="apitoken" type="string" %}
Tus credenciales de acceso
{% endswagger-parameter %}

{% swagger-response status="200" description="En caso de existir algún error, se retornará el campo "error" = "S" y dentro de "errores" una lista con todos los errores encontrados.
" %}
```
{
	"error": "N",
	"errores": [""],
	"rta": "OK",
	"resultados": [{
		"fecha": "11\/05\/2017",
		"concepto": "FACTURA A 0002-00000001 (CUIT DE PRUEBA)",
		"debe": 112.1,
		"haber": 0,
		"resta_abonar_de_este_comprobante": 112.1,
		"saldo": 112.1
	}, {
		"fecha": "11\/05\/2017",
		"concepto": "FACTURA A 0002-00000002 (CUIT DE PRUEBA)",
		"debe": 112.1,
		"haber": 0,
		"resta_abonar_de_este_comprobante": 112.1,
		"saldo": 224.2
	}]
 
}
```
{% endswagger-response %}
{% endswagger %}

### Ejemplo del JSON que debes enviar&#x20;

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

Se devolverá una lista, conteniendo la siguiente estructura,  con cada uno de los registros de la cuenta corriente de tu cliente.

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

