---
description: >-
  Consulta el estado de un cuit en la base provista por el Banco Central de la
  República Argentina (BCRA)
---

# API BCRA - Consulta de cheques rechazados por CUIT

### Consultar datos de un CUIT en base de cheques rechazados del Banco Central de la República Argentina (BCRA)

El servicio provisto por el BCRA te permite consultar la cantidad de cheques rechazados y el monto que éstos tengan

#### ¿A donde enviar el request?

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/padrones/`<mark style="color:purple;">**`bcra-cheques-rechazados`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request = 1 llamada`\
Los requests se cuentan individualmente por cada método que consumas [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

#### Request Body

| Name      | Type     | Description                                 |
| --------- | -------- | ------------------------------------------- |
| cuit      | numerico | Numero de hasta 11 digitos. Ej: 30000000001 |
| apikey    | string   | Tus credenciales de acceso                  |
| usertoken | string   | Tus credenciales de acceso.                 |
| apitoken  | string   | Tus credenciales de acceso.                 |
|           |          |                                             |

{% hint style="warning" %}
El servicio provisto por el BCRA funciona de manera inestable. En caso que no podamos conectar con la entidad, recibirás un mensaje de error.
{% endhint %}

#### Ejemplo del JSON a enviar <a href="#estructura-del-json-a-enviar" id="estructura-del-json-a-enviar"></a>

{% code title="JSON" %}
```json
{
"usertoken" :  "xxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxx",
"cuit"      :  30000000001
 }
```
{% endcode %}

#### Respuesta exitosa _(http code = 200)_ con CUIT existente en base BCRA _(http code = 200)_&#x20;

```json
{
	"error": "N",
	"errores": [],
	"cuit": xxxxxx,
	"existe_padron": "S",
	"detalle": []
}
```

#### Respuesta exitosa _(http code = 200)_  con CUIT inexistente en base BCRA _(http code = 200)_&#x20;

```json
{
	"error": "N",
	"errores": [],
	"cuit": xxxxxx,
	"existe_padron": "N" 
}
```

#### Respuesta con error _(http code = 200)_&#x20;

```json
{
	"error": "S",
	"errores": [
		"El cuit enviado (0) es invalido."
	]
}
```

