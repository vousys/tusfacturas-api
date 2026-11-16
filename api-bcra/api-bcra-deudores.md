---
description: >-
  Consulta en tiempo real la Central de Deudores del BCRA por CUIT o CUIL.
  Verifica situación crediticia, morosidad, entidades financieras y montos
  adeudados.
---

# API BCRA - deudores

Permite obtener el estado financiero informado por entidades bancarias y crediticias ante el BCRA, detallando la clasificación de situación (1 a 6), los montos adeudados y el período vigente.

#### ¿A donde enviar el request?

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/padrones/`<mark style="color:purple;">**`bcra-deudores`**</mark>
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

<pre class="language-json"><code class="lang-json"><strong>{
</strong>	"error": "N",
	"errores": [],
	"cuit": 20000000001,
	"riesgo_existe": false,
	"riesgo_situacion": 1,
	"detalle": {
		"identificacion": 20000000001, 
		"denominacion": "FEDERICO T",
		"periodos": [
			{
				"periodo": 202609,
				"entidades": [
					{
						"entidad": "BANCO DE LA NACION ARGENTINA",
						"situacion": 1,
						"fechaSit1": "2022-10-30",
						"monto": 507526,
						"diasAtrasoPago": 0,
						"refinanciaciones": false,
						"recategorizacionOblig": false,
						"situacionJuridica": false,
						"irrecDisposicionTecnica": false,
						"enRevision": false,
						"procesoJud": false
					},
					{
						"entidad": "BANCO DEL SOL S.A.",
						"situacion": 1,
						"fechaSit1": "2022-10-30",
						"monto": 118612,
						"diasAtrasoPago": 0,
						"refinanciaciones": false,
						"recategorizacionOblig": false,
						"situacionJuridica": false,
						"irrecDisposicionTecnica": false,
						"enRevision": false,
						"procesoJud": false
					},
					{
						"entidad": "BANCO DE LA PAMPA SA",
						"situacion": 1,
						"fechaSit1": "2022-10-30",
						"monto": 189381,
						"diasAtrasoPago": 0,
						"refinanciaciones": false,
						"recategorizacionOblig": false,
						"situacionJuridica": false,
						"irrecDisposicionTecnica": false,
						"enRevision": false,
						"procesoJud": false
					},
					{
						"entidad": "BANCO DE GALICIA Y BUENOS AIRES S.A.",
						"situacion": 1,
						"fechaSit1": "2022-10-30",
						"monto": 195183,
						"diasAtrasoPago": 0,
						"refinanciaciones": false,
						"recategorizacionOblig": false,
						"situacionJuridica": false,
						"irrecDisposicionTecnica": false,
						"enRevision": false,
						"procesoJud": false
					},
					{
						"entidad": "TOYOTA COMPAÑÍA FINANCIERA DE ARGENTINA S.A.",
						"situacion": 1,
						"fechaSit1": "2022-10-30",
						"monto": 10308,
						"diasAtrasoPago": 0,
						"refinanciaciones": false,
						"recategorizacionOblig": false,
						"situacionJuridica": false,
						"irrecDisposicionTecnica": false,
						"enRevision": false,
						"procesoJud": false
					},
					{
						"entidad": "BANCO MACRO S.A.",
						"situacion": 1,
						"fechaSit1": "2022-10-30",
						"monto": 136982,
						"diasAtrasoPago": 0,
						"refinanciaciones": false,
						"recategorizacionOblig": false,
						"situacionJuridica": false,
						"irrecDisposicionTecnica": false,
						"enRevision": false,
						"procesoJud": false
					},
					{
						"entidad": "ASOCIACION MUTUAL 23 DE SEPTIEMBRE",
						"situacion": 1,
						"fechaSit1": "2022-10-30",
						"monto": 43179,
						"diasAtrasoPago": 0,
						"refinanciaciones": false,
						"recategorizacionOblig": false,
						"situacionJuridica": false,
						"irrecDisposicionTecnica": false,
						"enRevision": false,
						"procesoJud": false
					}
				]
			}
		]
	}
}

</code></pre>

#### Respuesta exitosa _(http code = 200)_  con CUIT inexistente en base BCRA _(http code = 200)_&#x20;

```json
{
	"error": "N",
	"errores": [],
	"cuit": 20000000001,
	"riesgo_existe": false,
	"riesgo_situacion": 0,
	"detalle": []
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
