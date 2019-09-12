# Clientes - Cuenta Corriente

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="v2/clientes/cuenta-corriente" %}
{% api-method-summary %}
Consulta de cuenta corriente
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="cliente" required=true type="object" %}
**documento\_tipo**    Valores Permitidos: CUIT   
**documento\_nro**    Campo numérico, sin puntos ni guiones. Ejemplo: 30111222334
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=false %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de existir algún error, se retornará el campo "error" = "S" y dentro de "errores" una lista con todos los errores encontrados.  
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON que debes enviar 

```text
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

| `documento_tipo` | Valores Permitidos: **CUIT** **Ejemplo: CUIT** |
| :--- | :--- |
| `documento_nro` | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |

### Estructura de los datos devueltos

Se devolverá una lista, conteniendo la siguiente estructura,  con cada uno de los registros de la cuenta corriente de tu cliente.

```text
    {
        "fecha":"11\/05\/2017",
        "concepto":"FACTURA A 0002-00000002 (CUIT DE PRUEBA)",
        "debe":112.1,
        "haber":0,
        "resta_abonar_de_este_comprobante":112.1,
        "saldo":224.2
    }
```



