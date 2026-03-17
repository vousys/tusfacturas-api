---
description: >-
  Consulta la información básica de tu cliente, desde la constancia de
  inscripción de AFIP/ARCA, y obtené los datos en formato JSON.
---

# Consultar base APOC de facturas apócrifas de ARCA

### Consultar datos de un CUIT en base APOC

Este endpoint permite [consultar la base de datos APOC de ARCA](https://ayuda.tusfacturas.app/es/articles/12097418-que-son-las-facturas-apocrifas-y-como-verificarlas) para verificar si una factura está registrada como apócrifa o fraudulenta.

**Valida la autenticidad de facturas antes de procesarlas contablemente**, cumpliendo con las regulaciones fiscales argentinas y evitando la aceptación de comprobantes falsos que podrían generar observaciones de AFIP.

#### ¿A donde enviar el request?

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`padrones/apoc`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

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
```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxx",
"apitoken"  :  "xxxx",
"cuit"      :  30000000001
 }
```
{% endcode %}

#### Respuesta exitosa (200) con CUIT existente en base APOC

```
{
	"error": "N",
	"errores": [],
	"cuit": xxxxxx,
	"existe_padron": "S",
	"fecha_condicion_apocrifo": "04/12/2007",
	"fecha_publicacion": "04/12/2007",
	"base_actualizada_fecha": "26/08/2025 18:42"
}
```

#### Respuesta exitosa (200) con CUIT inexistente en base APOC

```
{
	"error": "N",
	"errores": [],
	"cuit": xxxxxx,
	"existe_padron": "N",
	"base_actualizada_fecha": "26/08/2025 18:42"
}
```

#### Respuesta con error (200) &#x20;

```
{
	"error": "S",
	"errores": [
		"El cuit enviado (0) es invalido."
	]
}
```

