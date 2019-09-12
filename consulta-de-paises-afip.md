# Consulta de Paises - AFIP

{% api-method method="post" host="https://www.tusfacturas.app/app/api" path="v2/tablas\_referencia/paises" %}
{% api-method-summary %}
Consulta de paises 
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de no existir errores, se devolverá la variable error con un valor "N" ademas de las variables que enunciamos a continuación.  
  
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```
 {
	"error": "N",
	"errores": [""],
	"items": [{
		"id": "250",
		"descripcion": "AAE Tierra del Fuego - ARGENTINA"
	}, {
		"id": "301",
		"descripcion": "AFGANISTAN"
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Estructura del JSON a enviar

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
	"usertoken": "jajajja8c8bf67c884e1405e26c03c85",
	"apikey": "9991",
	"apitoken": "kkakak208a17cdfc4e4741437baddaa6"
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

