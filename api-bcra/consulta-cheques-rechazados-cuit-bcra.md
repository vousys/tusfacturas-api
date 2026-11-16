---
description: >-
  Consulta el estado de un cuit en la base provista por el Banco Central de la
  República Argentina (BCRA)
---

# API BCRA - Consulta de cheques rechazados por CUIT

Este método API te devuelve la información oficial del BCRA asociada a un número de CUIT/CUIL, desglosando cada cheque rechazado por causal, entidad financiera, monto y fecha.

#### ¿A donde enviar el request?

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/padrones/`<mark style="color:purple;">**`bcra-cheques`**</mark>
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
	"cuit": 20000000001,
	"existe_padron": "S",
	"cheques_rechazados": 114,
	"detalle": {
		"identificacion": 20000000001,
		"denominacion": "FEDERICTO T",
		"causales": [
			{
				"causal": "SIN FONDOS",
				"entidades": [
					{
						"entidad": 1,
						"detalle": [
							{
								"nroCheque": 606,
								"fechaRechazo": "2026-11-02",
								"monto": 5000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 607,
								"fechaRechazo": "2026-11-03",
								"monto": 5000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 627,
								"fechaRechazo": "2026-11-03",
								"monto": 4950000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 680,
								"fechaRechazo": "2026-11-03",
								"monto": 2500000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 683,
								"fechaRechazo": "2026-11-03",
								"monto": 1500000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 737,
								"fechaRechazo": "2026-11-02",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 742,
								"fechaRechazo": "2026-11-03",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 760,
								"fechaRechazo": "2026-11-02",
								"monto": 1666666.6699999999,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 822,
								"fechaRechazo": "2026-11-02",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 823,
								"fechaRechazo": "2026-11-02",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 824,
								"fechaRechazo": "2026-11-03",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 825,
								"fechaRechazo": "2026-11-03",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 915,
								"fechaRechazo": "2026-11-03",
								"monto": 320000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 951,
								"fechaRechazo": "2026-11-03",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 979,
								"fechaRechazo": "2026-11-03",
								"monto": 1656036,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 996,
								"fechaRechazo": "2026-11-03",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1027,
								"fechaRechazo": "2026-11-02",
								"monto": 4643265.25,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1140,
								"fechaRechazo": "2026-11-03",
								"monto": 108000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1169,
								"fechaRechazo": "2026-11-02",
								"monto": 4290880.75,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1220,
								"fechaRechazo": "2026-11-03",
								"monto": 1295000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 826,
								"fechaRechazo": "2026-11-04",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-04",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 827,
								"fechaRechazo": "2026-11-04",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-04",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 679,
								"fechaRechazo": "2026-10-30",
								"monto": 2500000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-30",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 820,
								"fechaRechazo": "2026-10-30",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-30",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 821,
								"fechaRechazo": "2026-10-30",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-30",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 995,
								"fechaRechazo": "2026-10-30",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-30",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1026,
								"fechaRechazo": "2026-10-30",
								"monto": 4643265.25,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-30",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 818,
								"fechaRechazo": "2026-10-29",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-29",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 819,
								"fechaRechazo": "2026-10-29",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-29",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 994,
								"fechaRechazo": "2026-10-29",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-29",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1033,
								"fechaRechazo": "2026-10-29",
								"monto": 164333.32999999999,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-29",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1035,
								"fechaRechazo": "2026-10-29",
								"monto": 1000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-29",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 574,
								"fechaRechazo": "2026-11-05",
								"monto": 5918393.5999999996,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-05",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 761,
								"fechaRechazo": "2026-11-05",
								"monto": 1666666.6499999999,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-05",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 828,
								"fechaRechazo": "2026-11-05",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-05",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 829,
								"fechaRechazo": "2026-11-05",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-05",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 111,
								"fechaRechazo": "2026-10-27",
								"monto": 4260000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 605,
								"fechaRechazo": "2026-10-27",
								"monto": 6474310,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 677,
								"fechaRechazo": "2026-10-27",
								"monto": 2500000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 741,
								"fechaRechazo": "2026-10-27",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 814,
								"fechaRechazo": "2026-10-27",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 815,
								"fechaRechazo": "2026-10-27",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 894,
								"fechaRechazo": "2026-10-27",
								"monto": 5159375,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 993,
								"fechaRechazo": "2026-10-27",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1071,
								"fechaRechazo": "2026-10-26",
								"monto": 3418540,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1145,
								"fechaRechazo": "2026-10-27",
								"monto": 5000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1146,
								"fechaRechazo": "2026-10-27",
								"monto": 5000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1156,
								"fechaRechazo": "2026-10-27",
								"monto": 1700000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1160,
								"fechaRechazo": "2026-10-27",
								"monto": 4290880.75,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1222,
								"fechaRechazo": "2026-10-27",
								"monto": 5000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-27",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 676,
								"fechaRechazo": "2026-10-26",
								"monto": 2500000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 736,
								"fechaRechazo": "2026-10-26",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 754,
								"fechaRechazo": "2026-10-26",
								"monto": 1150383.3300000001,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 812,
								"fechaRechazo": "2026-10-26",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 813,
								"fechaRechazo": "2026-10-26",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1041,
								"fechaRechazo": "2026-10-26",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1082,
								"fechaRechazo": "2026-10-26",
								"monto": 2600000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1138,
								"fechaRechazo": "2026-10-26",
								"monto": 3410000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-26",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1102,
								"fechaRechazo": "2026-10-29",
								"monto": 1166666.6699999999,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-29",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1292,
								"fechaRechazo": "2026-10-28",
								"monto": 701379,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-29",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 678,
								"fechaRechazo": "2026-10-28",
								"monto": 2500000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 816,
								"fechaRechazo": "2026-10-28",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 817,
								"fechaRechazo": "2026-10-28",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 895,
								"fechaRechazo": "2026-10-28",
								"monto": 5159375,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 936,
								"fechaRechazo": "2026-10-28",
								"monto": 2500000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1024,
								"fechaRechazo": "2026-10-28",
								"monto": 4643265.25,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1025,
								"fechaRechazo": "2026-10-28",
								"monto": 4643265.25,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1043,
								"fechaRechazo": "2026-10-28",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1056,
								"fechaRechazo": "2026-10-28",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1161,
								"fechaRechazo": "2026-10-28",
								"monto": 4290880.75,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1170,
								"fechaRechazo": "2026-10-28",
								"monto": 1875000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-10-28",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 507,
								"fechaRechazo": "2026-11-02",
								"monto": 3850000,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-02",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 573,
								"fechaRechazo": "2026-11-03",
								"monto": 5918393.5999999996,
								"fechaPago": null,
								"fechaPagoMulta": "2026-11-03",
								"estadoMulta": null,
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							}
						]
					},
					{
						"entidad": 2,
						"detalle": [
							{
								"nroCheque": 1913809,
								"fechaRechazo": "2026-11-02",
								"monto": 583333.32999999996,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65694697,
								"fechaRechazo": "2026-11-02",
								"monto": 320000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828392,
								"fechaRechazo": "2026-11-02",
								"monto": 1700000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864335,
								"fechaRechazo": "2026-11-02",
								"monto": 2160000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1913808,
								"fechaRechazo": "2026-11-05",
								"monto": 583333.32999999996,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1971362,
								"fechaRechazo": "2026-11-04",
								"monto": 3705203.1200000001,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65745859,
								"fechaRechazo": "2026-10-28",
								"monto": 1740000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828368,
								"fechaRechazo": "2026-10-28",
								"monto": 1000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864303,
								"fechaRechazo": "2026-10-28",
								"monto": 2500000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864314,
								"fechaRechazo": "2026-10-28",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1863463,
								"fechaRechazo": "2026-10-27",
								"monto": 6250000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1962987,
								"fechaRechazo": "2026-10-27",
								"monto": 391949.5,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 2000854,
								"fechaRechazo": "2026-10-27",
								"monto": 218525.09,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 2032391,
								"fechaRechazo": "2026-10-27",
								"monto": 361966.67999999999,
								"fechaPago": "2026-11-02",
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65637194,
								"fechaRechazo": "2026-10-27",
								"monto": 1433334,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828400,
								"fechaRechazo": "2026-10-27",
								"monto": 9000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828401,
								"fechaRechazo": "2026-10-27",
								"monto": 9000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828402,
								"fechaRechazo": "2026-10-27",
								"monto": 9000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828409,
								"fechaRechazo": "2026-10-27",
								"monto": 720000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864318,
								"fechaRechazo": "2026-10-27",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1913810,
								"fechaRechazo": "2026-11-12",
								"monto": 583333.32999999996,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1971364,
								"fechaRechazo": "2026-11-12",
								"monto": 3705203.1200000001,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1971365,
								"fechaRechazo": "2026-11-12",
								"monto": 3705203.1200000001,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1994723,
								"fechaRechazo": "2026-11-12",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864346,
								"fechaRechazo": "2026-11-12",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1971363,
								"fechaRechazo": "2026-11-11",
								"monto": 3705203.1200000001,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1999119,
								"fechaRechazo": "2026-11-11",
								"monto": 351455.72999999998,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 2018623,
								"fechaRechazo": "2026-11-11",
								"monto": 240700,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828404,
								"fechaRechazo": "2026-11-11",
								"monto": 6656437,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864338,
								"fechaRechazo": "2026-11-11",
								"monto": 2200000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1989494,
								"fechaRechazo": "2026-11-03",
								"monto": 625000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1994722,
								"fechaRechazo": "2026-11-03",
								"monto": 2000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1997641,
								"fechaRechazo": "2026-11-03",
								"monto": 526780,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 2044583,
								"fechaRechazo": "2026-11-03",
								"monto": 88260.110000000001,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828367,
								"fechaRechazo": "2026-11-03",
								"monto": 1000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65828408,
								"fechaRechazo": "2026-11-03",
								"monto": 3000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864308,
								"fechaRechazo": "2026-11-03",
								"monto": 600000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864336,
								"fechaRechazo": "2026-11-03",
								"monto": 1970000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 1863464,
								"fechaRechazo": "2026-10-29",
								"monto": 6250000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864328,
								"fechaRechazo": "2026-10-29",
								"monto": 6400000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							},
							{
								"nroCheque": 65864339,
								"fechaRechazo": "2026-10-29",
								"monto": 4000000,
								"fechaPago": null,
								"fechaPagoMulta": null,
								"estadoMulta": "IMPAGA",
								"ctaPersonal": true,
								"denomJuridica": null,
								"enRevision": false,
								"procesoJud": false
							}
						]
					}
				]
			}
		]
	}
}
```

#### Respuesta exitosa _(http code = 200)_  con CUIT inexistente en base BCRA _(http code = 200)_&#x20;

```json
{
	"error": "N",
	"errores": [],
	"cuit": 20000000001,
	"existe_padron": "N",
	"cheques_rechazados": 0,
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

