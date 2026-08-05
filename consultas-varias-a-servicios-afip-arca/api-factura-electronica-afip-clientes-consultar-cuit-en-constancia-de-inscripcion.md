---
description: >-
  Consulta la información básica de tu cliente, desde la constancia de
  inscripción de AFIP/ARCA, y obtené los datos en formato JSON.
---

# Consultar datos de un CUIT, desde la constancia de inscripción

{% hint style="info" %}
**IMPORTANTE**: Para utilizar esta consulta, tu CUIT debe estar **enlazado con ARCA**. Por lo tanto, esta funcionalidad **no está disponible** en el plan API DEV.
{% endhint %}

### Consultar datos de un CUIT en AFIP/ARCA

Mediante éste método podrás consultar la info que AFIP/ARCA tiene almacenada en su base de datos con relación a un CUIT. Ésta info es lo mismo que visualizas cuando haces una [consulta web a la constancia de inscripción](https://seti.afip.gob.ar/padron-puc-constancia-internet/ConsultaConstanciaAction.do).  Tene en cuenta que la información provista en éste método no tiene relación con la info de tus clientes que tengas almacenados en TusFacturasAPP.

#### ¿A donde enviar el request?

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`clientes/afip-info`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

{% hint style="info" %}
**¿Necesitas consultar muchos CUITs a la vez?**

Si en lugar de integrar este método por API preferís hacer consultas masivas sin programar, podes usar la herramienta **"**[**Consulta masiva desde Excel de datos ARCA, ARBA, AGIP y APOC**](https://www.tusfacturas.app/consultar-cuits-en-arca-arba-agip-apoc-masivamente.html)**"** disponible en la plataforma web (menú > ARCA y padrones). Con ella podes cargar un archivo CSV con varios CUITs y obtener un reporte consolidado, sin necesidad de consultarlos uno por uno.

👉 [Ver cómo usar la consulta masiva desde Excel](https://ayuda.tusfacturas.app/es/articles/16221224-consulta-masiva-desde-excel-de-datos-arca-arba-agip-y-apoc)

⚠️ Los créditos disponibles para este método de API (`clientes/afip-info`) son **compartidos** con los que se consumen en la herramienta de consulta masiva. No existen saldos independientes: cada consulta, ya sea por API o desde el Excel masivo, descuenta del mismo saldo de créditos de tu plan.
{% endhint %}

#### Request Body

| Name      | Type   | Description                 |
| --------- | ------ | --------------------------- |
| cliente   | string | Objeto de tipo cliente      |
| apikey    | string | Tus credenciales de acceso  |
| usertoken | string | Tus credenciales de acceso. |
| apitoken  | string | Tus credenciales de acceso. |

#### Ejemplo del JSON a enviar <a href="#estructura-del-json-a-enviar" id="estructura-del-json-a-enviar"></a>

{% code title="JSON" %}
```json
{
"usertoken" :  "xxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxx",
"cliente":  {                      
    "documento_nro":    "30712293841",      
    "documento_tipo":   "CUIT"                   
    } 
 }
```
{% endcode %}

### Estructura del bloque "Cliente" <a href="#estructura-de-cliente" id="estructura-de-cliente"></a>

| `documento_tipo` | Valores Permitidos: **CUIT**                                    |
| ---------------- | --------------------------------------------------------------- |
| `documento_nro`  | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |

#### Ejemplo del JSON de respuesta exitosa

**Consulta de CUIT en constancia de inscripción ARCA para un monotributista:**

```json
{
   "error":             "N",
   "razon_social":      "LA RAZON SOCIAL O NOMBRE",
   "condicion_impositiva": "MONOTRIBUTO",
   "direccion": "xxxxx",
   "localidad": "",
   "codigopostal": "xxx",
   "estado":"ACTIVO",
   "provincia": "CIUDAD AUTONOMA BUENOS AIRES",
   "actividad":[
		{
			"descripcion": "SERVICIOS DE CONTABILIDAD, AUDITORÃA Y ASESORÃA FISCAL",
			"id": 692000,
			"nomenclador": 883,
			"periodo": 201311
		},
		{
			"descripcion": "SERVICIOS DE ASESORAMIENTO, DIRECCIÃN Y GESTIÃN EMPRESARIAL REALIZADOS POR INTEGRANTES DE CUERPOS DE DIRECCIÃN EN SOCIEDADES EXCEPTO LAS ANÃNIMAS",
			"id": 702092,
			"nomenclador": 883,
			"periodo": 201812
		}
   ],
   "apoc_existe": "SI",
   "apoc_info": "CUIT en base APOC desde el 22/07/2019.  (base APOC actualizada al 26/08/2025 18:42) -  Sugerimos consultar con su estudio contable inmediatamente.",
   "errores":  [  "" ] ,
   "constancia_full_datos": {
		"datosGenerales": {
			"apellido": "XXXXX",
			"caracterizacion": {
				"descripcionCaracterizacion": "GANANCIAS SIMPLIFICADA LEY 27.779",
				"fechaSolicitud": 20260712,
				"idCaracterizacion": 639,
				"periodo": 20250101
			},
			"domicilioFiscal": {
				"codPostal": 0,
				"descripcionProvincia": "CIUDAD AUTONOMA BUENOS AIRES",
				"direccion": "XXXXX",
				"idProvincia": 0,
				"tipoDomicilio": "FISCAL"
			},
			"esSucesion": "NO",
			"estadoClave": "ACTIVO",
			"idPersona": 0,
			"mesCierre": 12,
			"nombre": "XXXXX",
			"tipoClave": "CUIT",
			"tipoPersona": "FISICA"
		},
		"datosMonotributo": {
			"actividad": [
				{
					"descripcionActividad": "SERVICIOS DE CONTABILIDAD, AUDITORÍA Y ASESORÍA FISCAL",
					"idActividad": 692000,
					"nomenclador": 883,
					"orden": 1,
					"periodo": 201311
				},
				{
					"descripcionActividad": "SERVICIOS DE ASESORAMIENTO, DIRECCIÓN Y GESTIÓN EMPRESARIAL REALIZADOS POR INTEGRANTES DE CUERPOS DE DIRECCIÓN EN SOCIEDADES EXCEPTO LAS ANÓNIMAS",
					"idActividad": 702092,
					"nomenclador": 883,
					"orden": 2,
					"periodo": 201812
				}
			],
			"actividadMonotributista": {
				"descripcionActividad": "SERVICIOS DE CONTABILIDAD, AUDITORÍA Y ASESORÍA FISCAL",
				"idActividad": 692000,
				"nomenclador": 883,
				"orden": 1,
				"periodo": 201311
			},
			"categoriaMonotributo": {
				"descripcionCategoria": "F LOCACIONES DE SERVICIOS",
				"idCategoria": 40,
				"idImpuesto": 20,
				"periodo": 202508
			},
			"impuesto": {
				"descripcionImpuesto": "MONOTRIBUTO",
				"estadoImpuesto": "AC",
				"idImpuesto": 20,
				"motivo": "INSCRIPCIÓN TRAMITADA EN AGENCIA",
				"periodo": 200704
			}
		},
		"datosRegimenGeneral": {
			"actividad": [
				{
					"descripcionActividad": "SERVICIOS DE CONTABILIDAD, AUDITORÍA Y ASESORÍA FISCAL",
					"idActividad": 692000,
					"nomenclador": 883,
					"orden": 1,
					"periodo": 201311
				},
				{
					"descripcionActividad": "SERVICIOS DE ASESORAMIENTO, DIRECCIÓN Y GESTIÓN EMPRESARIAL REALIZADOS POR INTEGRANTES DE CUERPOS DE DIRECCIÓN EN SOCIEDADES EXCEPTO LAS ANÓNIMAS",
					"idActividad": 702092,
					"nomenclador": 883,
					"orden": 2,
					"periodo": 201812
				}
			],
			"categoriaAutonomo": {
				"descripcionCategoria": "T1 CAT III INGRESOS HASTA $15.000",
				"idCategoria": 103,
				"idImpuesto": 308,
				"periodo": 201811
			},
			"impuesto": [
				{
					"descripcionImpuesto": "IVA EXENTO",
					"estadoImpuesto": "AC",
					"idImpuesto": 32,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 201812
				},
				{
					"descripcionImpuesto": "GANANCIAS PERSONAS FISICAS",
					"estadoImpuesto": "AC",
					"idImpuesto": 11,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 201811
				},
				{
					"descripcionImpuesto": "APORTES SEG.SOCIAL AUTONOMOS",
					"estadoImpuesto": "AC",
					"idImpuesto": 308,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 201811
				},
				{
					"descripcionImpuesto": "REG. SIMPLIFICADO IIBB AGIP",
					"estadoImpuesto": "NA",
					"idImpuesto": 5190,
					"motivo": "NO ALCANZADO EN TRÁMITE EN LA JURISDICCIÓN",
					"periodo": 202601
				},
				{
					"descripcionImpuesto": "CONTRIBUCION MUNICIPAL AGIP",
					"estadoImpuesto": "NA",
					"idImpuesto": 5191,
					"motivo": "JURISDICCIÓN NO ADHERIDA",
					"periodo": 202601
				}
			]
		},
		"metadata": {
			"fechaHora": "2026-07-23T06:02:58.172-03:00",
			"servidor": "linux11f"
		}
	},
}	
```

**Consulta de CUIT en constancia de inscripción ARCA para un responsable inscripto:**

```json
{
	"error": "N",
	"errores": [],
	"razon_social": "XXXX",
	"condicion_impositiva": "RESPONSABLE INSCRIPTO",
	"direccion": "XXXX",
	"localidad": "",
	"codigopostal": "XXX",
	"provincia": "CIUDAD AUTONOMA DE BUENOS AIRES",
	"estado": "ACTIVO",
	"actividad": [
		{
			"descripcion": "SERVICIOS DE CONSULTORES EN INFORMÃTICA Y SUMINISTROS DE PROGRAMAS DE INFORMÃTICA",
			"id": 620100,
			"nomenclador": 883,
			"periodo": 201812
		},
		{
			"descripcion": "SERVICIOS EMPRESARIALES N.C.P.",
			"id": 829900,
			"nomenclador": 883,
			"periodo": 201906
		}
	],
	"constancia_full_datos": {
		"datosGenerales": {
			"domicilioFiscal": {
				"codPostal": 0,
				"datoAdicional": "XXXX",
				"descripcionProvincia": "CIUDAD AUTONOMA BUENOS AIRES",
				"direccion": "XXXX",
				"idProvincia": 0,
				"tipoDatoAdicional": "XXXX",
				"tipoDomicilio": "FISCAL"
			},
			"esSucesion": "NO",
			"estadoClave": "ACTIVO",
			"fechaContratoSocial": "2018-11-01T12:00:00-03:00",
			"idPersona": 0,
			"mesCierre": 10,
			"razonSocial": "XXXX",
			"tipoClave": "CUIT",
			"tipoPersona": "JURIDICA"
		},
		"datosRegimenGeneral": {
			"actividad": [
				{
					"descripcionActividad": "SERVICIOS DE CONSULTORES EN INFORMÁTICA Y SUMINISTROS DE PROGRAMAS DE INFORMÁTICA",
					"idActividad": 620100,
					"nomenclador": 883,
					"orden": 1,
					"periodo": 201812
				},
				{
					"descripcionActividad": "SERVICIOS EMPRESARIALES N.C.P.",
					"idActividad": 829900,
					"nomenclador": 883,
					"orden": 2,
					"periodo": 201906
				}
			],
			"impuesto": [
				{
					"descripcionImpuesto": "REGIMENES DE INFORMACIÓN",
					"estadoImpuesto": "AC",
					"idImpuesto": 103,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 201812
				},
				{
					"descripcionImpuesto": "IVA",
					"estadoImpuesto": "AC",
					"idImpuesto": 30,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 201812
				},
				{
					"descripcionImpuesto": "GANANCIAS SOCIEDADES",
					"estadoImpuesto": "AC",
					"idImpuesto": 10,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 201812
				},
				{
					"descripcionImpuesto": "BP-ACCIONES O PARTICIPACIONES",
					"estadoImpuesto": "AC",
					"idImpuesto": 211,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 201812
				},
				{
					"descripcionImpuesto": "EMPLEADOR-APORTES SEG. SOCIAL",
					"estadoImpuesto": "AC",
					"idImpuesto": 301,
					"motivo": "INSCRIPCIÓN NO TRAMITADA EN AGENCIA",
					"periodo": 202604
				}
			],
			"regimen": [
				{
					"descripcionRegimen": "PARTICIPACIONES SOCIETARIAS",
					"idImpuesto": 103,
					"idRegimen": 68,
					"periodo": 20181201
				},
				{
					"descripcionRegimen": "PRESENTACION DE ESTADOS CONTABLES EN FORMATO PDF",
					"idImpuesto": 103,
					"idRegimen": 255,
					"periodo": 20181101
				}
			]
		},
		"metadata": {
			"fechaHora": "2026-07-23T06:30:20.970-03:00",
			"servidor": "linux11e"
		}
	},
	"apoc_existe": "NO",
	"apoc_info": ""
}
```

{% hint style="info" %}
El campo `constancia_full_datos` contiene la respuesta completa y sin modificar devuelta por ARCA, permitiendo el acceso a datos adicionales para integraciones secundarias.

> Nota: La estructura de este objeto está sujeta a modificaciones según los cambios que realice ARCA en sus servicios.
{% endhint %}

#### Ejemplo de respuesta cuando ARCA  bloquea la constancia de inscripción:

```json
{
	"error": "S",
	"errores": [
		[
			"El servicio de consulta de CUIT en AFIP retorna el siguiente error:   - La CUIT registra pendiente la constitución del domicilio fiscal electrónico de acuerdo a lo normado en la RG 4280/18 AFIP.,La CUIT registra una o más actividades económicas que no pertenecen al nomenclador de actividades vigente F. 883 RG AFIP3587/13."
		]
	]
}
```

#### Ejemplo de respuesta, cuando el CUIT no tiene impuestos asociados en ARCA y no se puede determinar su condición fiscal

```json
{
	"error": "S",
	"errores": [
		"No se ha podido recuperar la condicion frente al IVA de este CUIT"
	],
	"razon_social": "CONSORCIO DE COPROPIETARIOS XXX",
	"condicion_impositiva": "CONSUMIDOR FINAL",
	"direccion": "XXXX 179",
	"localidad": "LOMAS DE ZAMORA",
	"codigopostal": "CP: 1832",
	"provincia": "BUENOS AIRES",
	"estado": "ACTIVO",
	"actividad": [
		{
			"descripcion": "SERVICIOS DE CONSORCIOS DE EDIFICIOS",
			"id": 949920,
			"nomenclador": 883,
			"periodo": 201311
		}
	],
	"apoc_existe": "NO",
	"apoc_info": ""
}
```

#### "condicion\_impositiva": Posibles valores de la respuesta obtenida desde ARCA.

El campo  `condicion_impositiva` puede retornar alguno de los siguientes valores:

* MONOTRIBUTO
* EXENTO
* RESPONSABLE INSCRIPTO

{% hint style="info" %}
Ten en cuenta que:

1. &#x20;Si el CUIT no se encuentra inscripto en ningún impuesto, nuestra plataforma te devolverá los datos que ésta encuentra en ARCA,  pero el campo "error"  en "S", ya que no podemos determinar que la condición frente al IVA.
2. Si el CUIT que estas consultando tiene requerimientos pendientes por responder o alguna otra inconsistencia en AFIP, el propio organismo bloquea el acceso a la información de su constancia y recibirás un error.
3. Generalmente para los responsables inscriptos ARCA no informa todos los datos catastrales. Podes corroborar la info que te devolvemos accediendo a la [consulta de inscripción de ARCA](https://seti.afip.gob.ar/padron-puc-constancia-internet/ConsultaConstanciaAction.do)
{% endhint %}
