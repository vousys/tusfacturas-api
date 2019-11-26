# Consulta de comprobantes y regeneración de PDF

Tipo de datos: **JSON**  
Charset: **UTF-8**

{% api-method method="post" host="https://www.tusfacturas.app/app/api/" path="v2/facturacion/consulta " %}
{% api-method-summary %}
Consulta de comprobantes 
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="comprobante" required=true %}
**tipo**    Campo numérico según tabla de referencia de Tipos de comprobantes\(\*\*\*\). Ejemplo: FACTURA B **operacion**    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V   
**punto\_venta**    Campo numérico entero. Longitud máxima 4 digitos. Ejemplo: 3   
**numero**    Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante. Ejemplo: 4567
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso.  
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=true %}
Tus Credenciales de acceso.  
{% endapi-method-parameter %}

{% api-method-parameter name="usertoken" type="string" required=true %}
Tus Credenciales de acceso.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
En caso de respuesta exitosa el campo "error" retornará una "S" y en caso de error una "N" y dentro de errores, una lista con cada uno de los errores encontrados.  
La estructura de los datos devueltos es igual a la envidada para la generación de los comprobantes.  
  
A continuación se visualiza un ejemplo del JSON retornado para el comprobante consultado.  
  
Importante:   
  
-  Los campos numéricos son retornados como número, salvo el CAE y el CUIT  
-  Para comprobantes tipo B, el precio ya incluye la alícuota de IVA calculada.  
  
{% endapi-method-response-example-description %}

{% tabs %}
{% tab title="JSON" %}
```
{
	"error": "N",
	"errores": [""]
	"rta": "OK",
	"cliente": {
		"documento_tipo": "DNI",
		"documento_nro": "1292963535 ",
		"razon_social": "Pirulo",
		"email": "test@test.com",
		"domicilio": "Av Sta Fe 123"
	},
	"comprobante": {
		"fecha": "28\/07\/2015",
		"tipo": "NOTA DE DEBITO B",
		"moneda": "PES",
		"idioma": 1,
		"cotizacion": 1,
		"operacion": "V",
		"punto_venta": 2,
		"numero": 6,
		"periodo_facturado_desde": "27\/07\/2015",
		"periodo_facturado_hasta": "30\/07\/2015",
		"rubro": "Servicios web",
		"rubro_grupo_contable": "servicios",
		"detalle": [{
			"cantidad": 1,
			"producto": {
				"descripcion": "PAPAS",
				"precio_unitario": 121.54,
				"alicuota": 21,
				"unidad_medida": 7,
				"precio_total": 121.54
 			},
			"leyenda": "blanca, cepillada"
		}, {
			"cantidad": 1.5,
			"producto": {
				"descripcion": "HUEVOS",
				"precio_unitario": 60.50,
				"alicuota": 21,
				"unidad_medida": 7,
				"precio_total": 90.75
				
			},
			"leyenda": ""
		}, {
			"cantidad": 2,
			"producto": {
				"descripcion": "ZANAHORIA",
				"precio_unitario": 242,
				"alicuota": 21,
				"unidad_medida": 7,
				"precio_total": 484 
           },
			"leyenda": ""
		}, ],
		"bonificacion": 120,
		"subtotal_1":  380.45,
		"iva_alicuota": 21,
		"subtotal_2": 75,
		"iva_alicuota_2": 10.5,
		"leyenda_gral": "bla bla bla",
        "percepciones_iibb":        "0",
        "percepciones_iibb_base":   "0",
        "percepciones_iibb_alicuota": "0",
        "percepciones_iva":         "0",
        "percepciones_iva_base":    "0",
        "percepciones_iva_alicuota": "0",
     	"exentos":                  "0",
        "impuestos_internos":       "0",
        "impuestos_internos_base":   "0",
        "impuestos_internos_alicuota": "0" ,
		"nogravados": 0,
		"total": 543.21,
		"cae": "65301278726386 ",
		"afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
		"vencimiento_cae": "07\/08\/2015",
		"vencimiento_pago": "27\/08\/2015",
		"comprobante_pdf_url": "https://www.dominio.com/00000006.pdf",
	}
}
```
{% endtab %}

{% tab title="Plain Text" %}
```

```
{% endtab %}
{% endtabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Los datos devueltos por éste método mantienen la misma estructura que los enviados para generar un comprobante.
{% endhint %}

### Ejemplo de JSON a enviar para consultar un comprobante:

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}

```

## Regenear PDF

Mediante éste método podrás regenerar los archivos pdf

{% api-method method="post" host="https://www.tusfacturas.app/app/api/" path="v2/facturacion/regenerar\_pdf " %}
{% api-method-summary %}
Regenerar PDFs
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="usertoken" type="string" required=false %}
tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apitoken" type="string" required=false %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="comprobante" required=true %}
**tipo**    Campo numérico según tabla de referencia de Tipos de comprobantes\(\*\*\*\). Ejemplo: FACTURA B   
**operacion**    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V   
**punto\_venta**    Campo numérico entero. Longitud máxima 4 digitos. Ejemplo: 3   
**numero**    Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante. Ejemplo: 4567
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Regenera el PDF y te devuelve la URL del archivo
{% endapi-method-response-example-description %}

```
{
"error" :  "N",
"comprobante_pdf_url"    :  "http://www.prueba.com"
}

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Ejemplo del JSON a enviar para regenerar el pdf

{% code title="JSON" %}
```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}


```
{% endcode %}

## Estructura de "Comprobante":

| `tipo` | Campo numérico según tabla de referencia de [Tipos de comprobantes\(\*\*\*\)](https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes). **Ejemplo: FACTURA B** |
| :--- | :--- |
| `operacion` | Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\).  Valores Permitidos: **V, C** **Ejemplo: V** |
| `punto_venta` | Campo numérico entero. Longitud máxima 4 digitos. **Ejemplo: 3** |
| `numero` | Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante. **Ejemplo: 4567** |

