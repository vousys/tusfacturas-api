# Facturación individual: Nuevo comprobante de Venta

{% hint style="info" %}
Poder utilizar la API debes [estar registrado](https://www.tusfacturas.com.ar/registrarme-factura-electronica.html). 

Mientras estés en etapa de testing, configurá tu CUIT con un punto de venta irreal \(Ej: 679\), y usa ese CUIT de prueba para facturar, la respuesta que recibirás es la misma que si facturas  contra AFIP, solo que los campos CAE y Vencimiento del CAE te retornaran vacios.  Una vez que hayas probado todos los métodos, crea el nuevo CUIT+punto de venta y lo enlazas con AFIP.

Ten en cuenta que al registrarte, te asignamos un plan gratuito que te permite emitir 5 comprobantes por mes y una vez vencido tu período de prueba, debes contratar algún plan API de los que tenemos disponibles aquí .

En caso que requieras 20 días con un plan free para el desarrollo, contáctanos a tusfacturas@vousys.com
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api/" path="v2/facturacion/nuevo" %}
{% api-method-summary %}
Nuevo comprobante de Venta
{% endapi-method-summary %}

{% api-method-description %}
Charset: UTF-8   
Tipo de dato esperado: JSON  
  
Éste metodo te permite generar comprobantes de venta, ya sea Facturas electrónicas AFIP, como Notas de débito o de crédito.  
Nuestra plataforma te permite emitir comprobantes de tipo A, B, C, E, M  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apisecret" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="comprobante" type="object" required=true %}
Estructura de "comprobante" según se informa a continuación
{% endapi-method-parameter %}

{% api-method-parameter name="cliente" type="object" required=true %}
Estructura de "Cliente", según se informa a continuación 
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Si el comprobante se ha podido generar sin problemas  se devolverá la variable "error" = "N".  
En caso de detectar error, la variable "error" contendrá una "S" y "errores" una lista con todos los errores encontrados   
  
Importante:  
  
- El CAE es el Código de Autorización Electrónico que otorga AFIP como confirmación de la creación del comprobante. Es un dato importante para almacenar como respuesta.  
  
- Los CAE tienen fecha de vencimiento y se devuelve en formato dd/mm/aaaa  
  
- El número de CAE es un texto y se envia con un espacio al final.  
  
- El texto que se retorna en el campo afip\_codigo\_barras se envía con un espacio al final.  
   
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```javascript
{
    "error":     "N",
     "errores": [ ""],    
     "rta":      "El comprobante NOTA DE DEBITO B 0002-00000006 (MI CUIT) se ha guardado correctamente",    
     "cae":      "65301278726386 ",    
     "vencimiento_cae":"07\/08\/2015",    
     "vencimiento_pago":"27\/08\/2015",    
     "comprobante_pdf_url": "https://www.dominio.com/url",
     "afip_codigo_barras" : "12121212121006000300000000000000201811052 ",
     "envio_x_mail": "S",
     "comprobante_nro": "0000123",
     "comprobante_tipo": "NOTA DE DEBITO B",
     "envio_x_mail_direcciones":"direccion1@sudominio.com,direccion2@sudominio.com"
  }  
  
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Ten en cuenta a la hora de calcular el total, que las bonificaciones están gravadas con IVA 
{% endhint %}

### Ejemplo de JSON para generar un comprobante.

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"cliente"   :
                {   "documento_tipo":       "DNI",
                    "documento_nro":        "1292963535",
                    "razon_social":         "Pirulo",
                    "email":                "test@test.com",
                    "domicilio":            "Av Sta Fe 123",
                    "provincia":            "2",
                    "envia_por_mail":       "S",
                    "condicion_pago":       "30",
                    "condicion_iva":        "CF"
                },

"comprobante":  {

                "fecha":                    "28\/07\/2015",
                "tipo":                     "NOTA DE DEBITO B",
                "moneda":                   "DOL",
               "idioma":                   "1",
                "cotizacion":               "15.20",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6",
                "periodo_facturado_desde":  "27\/07\/2015",
                "periodo_facturado_hasta":  "30\/07\/2015",
                "vencimiento":              "30\/08\/2015",
                "rubro":                    "Servicios web",
                "rubro_grupo_contable":     "servicios",
                "abono": "S",
                "abono_frecuencia": "2",
                "abono_hasta":"10/2019",
                "abono_actualiza_precios": "N",
                "detalle":
                            [
                                {
                                    "cantidad":"1",
                                    "afecta_stock": "N",
                                     "bonificacion_porcentaje": "0",
                                    "producto":
                                            {"descripcion":     "PAPAS",
                                             "unidad_bulto":    "10",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "",
                                             "precio_unitario_sin_iva":"100.45",
                                             "alicuota":      "21",
                                             "unidad_medida": "7",
                                             "actualiza_precio": "S"
                                             },
                                    "leyenda":"blanca, cepillada"
                                },


                                {
                                    "cantidad":"1.5",
                                     "bonificacion_porcentaje": "0",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "HUEVOS",
                                             "unidad_bulto":    "30",
                                             "lista_precios":   "MAPPLETS",
                                             "codigo":          "MPH",
                                             "precio_unitario_sin_iva":"50",
                                             "alicuota":      "10.5",
                                             "unidad_medida": "7",
                                             "actualiza_precio": "N"
                                             },
                                    "leyenda":""
                                },

                                {
                                    "cantidad":"2",
                                     "bonificacion_porcentaje": "0",
                                    "afecta_stock": "S",
                                    "producto":
                                            {"descripcion":     "ZANAHORIA",
                                             "unidad_bulto":    "50",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "ZNH1",
                                             "precio_unitario_sin_iva":"200",
                                             "alicuota":      "21",
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":""
                                }

                            ],
            "rg_especiales":
                 {   "regimen" : "RG 4004-E",
                      "datos"  : 

                           [{
                               "id"      :    17,
                               "valor"  :    "2"
                            },
                            {
                              "id"      :    1801,
                             "valor"  :    "111111111111"
                             },
                            {
                              "id"      :    1802,
                             "valor"  :    "PRUEBA"
                             }]
                },                          
                "bonificacion":             "120",
                "leyenda_gral":             "Segun Orden de compra III1333",
                "comentario":               "Factura correspondiente al servicio XX",
                "percepciones_iibb":        "0",
                "percepciones_iibb_base":   "0",
                "percepciones_iibb_alicuota": "0",
                "percepciones_iva":         "0",
                "percepciones_iva_base":    "0",
                "percepciones_iva_alicuota": "0",
                "exentos":                  "0",
                "nogravados":               "0",
                "impuestos_internos":       "0",
                "impuestos_internos_base":   "0",
                "impuestos_internos_alicuota": "0",
                "total":                    "543.22" 
                
        }
}


```

### Estructura de "Comprobante"

Para poder generar el comprobante, debes enviar de todos los datos según se informa a continuación.

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
   
"comprobante":  {

                "fecha":                    "28\/07\/2015",
                "tipo":                     "NOTA DE DEBITO B",
                "moneda":                   "DOL",
               "idioma":                   "1",
                "cotizacion":               "15.20",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6",
                "periodo_facturado_desde":  "27\/07\/2015",
                "periodo_facturado_hasta":  "30\/07\/2015",
                "vencimiento":              "30\/08\/2015",
                "rubro":                    "Servicios web",
                "rubro_grupo_contable":     "servicios",
                "abono": "S",
                "abono_frecuencia": "2",
                "abono_hasta":"10/2019",
                "abono_actualiza_precios": "N",
                "detalle":
                            [
                                {
                                    "cantidad":"1",
                                    "bonificacion_porcentaje": "0",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "PAPAS",
                                             "unidad_bulto":    "10",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "",
                                             "precio_unitario_sin_iva":"100.45",
                                             "alicuota":      "21",
                                             "unidad_medida": "7",
                                             "actualiza_precio": "S"
                                             },
                                    "leyenda":"blanca, cepillada"
                                },


                                {
                                    "cantidad":"1.5",
                                    "afecta_stock": "N",
                                     "bonificacion_porcentaje": "0",
                                    "producto":
                                            {"descripcion":     "HUEVOS",
                                             "unidad_bulto":    "30",
                                             "lista_precios":   "MAPPLETS",
                                             "codigo":          "MPH",
                                             "precio_unitario_sin_iva":"50",
                                             "alicuota":      "10.5",
                                             "unidad_medida": "7",
                                             "actualiza_precio": "N"
                                             },
                                    "leyenda":""
                                },

                                {
                                    "cantidad":"2",
                                    "afecta_stock": "S",
                                     "bonificacion_porcentaje": "0",
                                    "producto":
                                            {"descripcion":     "ZANAHORIA",
                                             "unidad_bulto":    "50",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "ZNH1",
                                             "precio_unitario_sin_iva":"200",
                                             "alicuota":      "21",
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":""
                                }

                            ],
                "bonificacion":             "120",
                "leyenda_gral":             "Segun Orden de compra III1333",
                "comentario":               "Factura correspondiente al servicio XX",
                "percepciones_iibb":        "0",
                "percepciones_iva":         "0",
                "exentos":                  "0",
                "nogravados":               "0",
                "impuestos_internos":       "0",
                "total":                    "543.22",
                "comprobantes_asociados":    []
        }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
Importante: **TusFacturas.app NO válida que la sumatoria de los ítems que estas enviando para facturar se correspondan con los totales. Es responsabilidad del cliente corroborar y validar éstos datos.** 

Recordá que AFIP recibe únicamente totales, no el detalle de los items que facturas ya que para los comprobantes de tipo "A" , "B" , "C" y "M" , TusFacturas.app utiliza el método de facturación mediante webservice AFIP "WSFEv1" \( Factura electrónica sin detalle de productos \).
{% endhint %}

#### Información de los campos a enviar:

| Nombre del campo | Requerido | Comentarios |
| :--- | :--- | :--- |
| fecha  | SI | Campo fecha. Para facturación afip deberá ser la fecha del día. Formato esperado: dd/mm/aaaa. Ejemplo: 13/05/2018 |
| tipo | SI | Campo alfabético según [tabla de referencia de Tipos de comprobantes](../tablas-de-referencia.md#tipos-de-comprobantes). |
| operacion | SI | Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V |
| idioma | SI | Campo numérico. Longitud 1 caracter. Indica el idioma en que se imprimira el PDF del comprobante. Valores Permitidos: 1 = Español, 2= Ingles |
| punto\_venta | SI | Campo numérico entero. Longitud máxima 5 digitos. |
| moneda | SI | Campo alfanumérico de 3 Digitos según [tabla de referencia de Monedas](../tablas-de-referencia.md#monedas) . |
| cotizacion | SI | Campo numérico con 2 decimales. Puede obtener la cotización del día según AFIP desde nuestro método de consulta de cotización Ejemplo: 15.20 |
| numero | OPCIONAL | El numero del comprobante a generar. Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante contra AFIP. Si el nro de comprobante NO es enviado, traeremos la próxima numeración . Ejemplo: 4567 |
| vencimiento | OPCIONAL | Campo fecha, formato esperado: dd/mm/aaaa. Si no se envía la fecha de vencimiento del pago, se calculará en base a la condición de pago del cliente, contra la fecha del comprobante. |
| periodo\_facturado\_desde | SI | Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y asi lo indiquen en la configuración de su CUIT+punto de venta. Obligatorio para quienes facturen Servicios o Productos y Servicios. |
| periodo\_facturado\_hasta | SI | Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y así lo indiquen en la configuración de su CUIT+punto de venta.Obligatorio para quienes facturen Servicios o Productos y Servicios. |
| rubro | SI |  Campo alfanumérico. Longitud máxima 255 caracteres. Indica el rubro al cual pertenecerá el comprobante. Ésta información no saldrá impresa en el comprobante. |
| rubro\_grupo\_contable | SI |  Campo alfanumérico. Longitud máxima 255 caracteres. Indica el grupo contable al que pertenece el rubro. Ésta información no saldrá impresa en el comprobante. |
| abono | OPCIONAL | Campo alfabético, longitud máxima 1 caracter. Valores permitidos S \(si\) o N \(no\). Indica si el comprobante a generar es un abono recurrente. |
| abono\_frecuencia | REQUERIDO SOLO SI ENVIA ABONO | Campo numerico sin decimales. Indica la frecuencia en meses con la que debe generarse la recurrencia del abono. |
| abono\_hasta | REQUERIDO SOLO SI ENVIA ABONO | Campo fecha \(mm/yyyy\). Longitud maxima 7. Indica el mes y año hasta el cual debe generarse el abono recurrente. |
| abono\_actualiza\_precios | REQUERIDO SOLO SI ENVIA ABONO | Campo alfabético, longitud máxima 1 caracter. Valores permitidos S \(si\) o N \(no\). Indica si cada vez que se genera el abono, se actualiza los precios de los productos contra el precio actual de la lista de precios. |
| detalle | SI |  Lista de conceptos a facturar. [Objeto JSON](./#estructura-de-detalle-de-conceptos) Según estructura que se detalla a continuación |
| fex | REQUERIDO PARA COMPROBANTES E | Solo para comprobantes de tipo E. Según estructura detallada en: [Factura electronica de exportacion".](factura-electronica-afip-exportacion.md) |
| bonificacion | OPCIONAL |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor aplicado en concepto de bonificación sin IVA Ejemplo: 12.67. Tener en cuenta para el cálculo que la bonificación se aplica sobre el primer subtotal SIN IVA y se lo gravará con el importe de IVA que le corresponda. |
| leyenda\_gral | OPCIONAL |  Campo alfanumérico. Longitud máxima 255 caracteres. Contenido opcional. Es una leyenda general que saldrá impresa en el bloque central de productos del comprobante Ejemplo: Aplica plan 12 cuotas sin interes. |
| comentario | OPCIONAL | Campo alfanumerico, opcional. Longitud máxima: 255 caracteres. Éste campo no saldrá impreso en la factura. |
| percepciones\_iibb | OPCIONAL |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de ingresos brutos realizada Ejemplo: 142.67 |
| percepciones\_iibb\_base | OPCIONAL | La base imponible  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67 |
| percepciones\_iibb\_alicuota | OPCIONAL | La alícuota  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67 |
| percepciones\_iva | OPCIONAL | Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de IVA realizada Ejemplo: 42.67 |
| percepciones\_iva\_base | OPCIONAL | La base imponible sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67 |
| percepciones\_iva\_alicuota | OPCIONAL | La alícuota  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67 |
| impuestos\_internos | OPCIONAL | Indica el valor monetario correspondiente a los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67 |
| impuestos\_internos\_base | OPCIONAL | La base imponible  sobre la cual se calcularon los impuestos internos. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67 |
| impuestos\_internos\_alicuota | OPCIONAL | La alícuota  sobre la cual se calculo la percepción. Campo numérico con 2 decimales. separador de decimales: punto. Ejemplo: 42.67 |
| exentos | OPCIONAL |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de exentos. Solo para comprobantes A y M Ejemplo: 72.67 |
| nogravados | OPCIONAL |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de no gravados. Solo para comprobantes A y M Ejemplo: 62.67 impuestos\_internos Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de impuestos internos Ejemplo: 2.67 |
| total | SI |  Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la sumatoria de conceptos incluyendo IVA e impuestos. Ejemplo: 12452.67 |
| comprobantes\_asociados | SEGUN CORRESPONDA | Lista de comprobantes asociados. Requerido únicamente para NC o ND de tipo A,B,C,M. [Objeto JSON](./#estructura-de-comprobantes-asociados) Según estructura que se detalla a continuación |
| rg\_especiales | SEGUN CORRESPONDA | Lista de datos adicionales requeridos por AFIP, según la RG a la que aplique el comprobante.  [Objeto JSON](./#estructura-de-rg-especiales) Según estructura que se detalla a continuación |

### Estructura de  "Cliente"

Para poder generar el comprobante, debes enviar un detalle de todos los datos del cliente según se informa a continuación.

```text
{   
"documento_tipo":       "DNI",
"documento_nro":        "1292963535",
"razon_social":         "Pirulo",
"email":                "test@test.com",
"domicilio":            "Av Sta Fe 123",
"provincia":            "2",
"envia_por_mail":       "S",
"condicion_pago":       "30",
"condicion_iva":        "CF"
}
```

{% hint style="info" %}
Si el cliente ya existia en la base de datos de www.tusfacturas.com.ar será actualizado con los nuevos datos, salvo Tipo y Nro de documento y condicion ante el IVA
{% endhint %}

#### Información de los campos a enviar:

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b><code>documento_tipo</code></b>
      </th>
      <th style="text-align:left">Valores Permitidos: <b>CUIT , DNI, PASAPORTE, OTRO</b>
        <br /><b>Ejemplo: DNI</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>documento_nro</code>
      </td>
      <td style="text-align:left">Campo num&#xE9;rico, sin puntos ni guiones.
        <br /><b>Ejemplo: 30111222334</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>razon_social</code>
      </td>
      <td style="text-align:left">Campo alfanum&#xE9;rico. Longitud m&#xE1;xima 255 caracteres.
        <br /><b>Ejemplo: Pirulo S.A</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>email</code>
      </td>
      <td style="text-align:left">Campo alfanum&#xE9;rico. Longitud m&#xE1;xima 255 caracteres.
        <br /><b>Ejemplo: tusfacturas@vousys.com</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>domicilio</code>
      </td>
      <td style="text-align:left">Campo alfanum&#xE9;rico. Longitud m&#xE1;xima 255 caracteres.
        <br /><b>Ejemplo: Av. Santa Fe 123</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>provincia</code>
      </td>
      <td style="text-align:left">Campo num&#xE9;rico seg&#xFA;n <a href="../tablas-de-referencia.md#provincias">tabla de referencia(*)</a>.
        <br
        /><b>Ejemplo: 2</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>envia_por_mail</code>
      </td>
      <td style="text-align:left">Indica Si/No para el envio del comprobante por e-mail. Valores Permitidos: <b>S , N</b>
        <br
        /><b>Ejemplo: S</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>condicion_pago</code>
      </td>
      <td style="text-align:left">
        <p>Campo num&#xE9;rico que indica la cantidad de dias en los cuales vence
          el plazo de pago y en base a &#xE9;ste valor se calcula la fecha de vencimiento
          del comprobante emitido.</p>
        <p>Valores Permitidos: <b>0,1,2,3,10,15,20,30,45,60,90.</b>
        </p>
        <p>0 = Contado</p>
        <p>15,30,60,90 = xx dias</p>
        <p>1 = Transferencia bancaria</p>
        <p>2 = Tarjeta Cr&#xE9;dito</p>
        <p>3= Tarjeta D&#xE9;bito</p>
        <p>
          <br /><b>Ejemplo: 30 </b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>condicion_iva</code>
      </td>
      <td style="text-align:left">Campo num&#xE9;rico que indica la condicion de iva, seg&#xFA;n <a href="../tablas-de-referencia.md#condiciones-ante-el-iva">tabla de referencia Condiciones ante el IVA(**)</a>.
        Valores Permitidos: <b>CF, RI, M, E </b>
        <br /><b>Ejemplo: RI</b>
      </td>
    </tr>
  </tbody>
</table>### Estructura de "Detalle de conceptos"

El detalle de conceptos se compone de una lista de cada uno de los productos que vas a facturar.

La estructura de cada concepto a enviar es la siguiente:

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
	"cantidad": "1.5",
	"afecta_stock": "N",
	"bonificacion_porcentaje": "0",
	"producto": {
		"descripcion": "HUEVOS",
		"unidad_bulto": "30",
		"lista_precios": "MAPPLETS",
		"codigo": "MPH",
		"precio_unitario_sin_iva": "50",
		"alicuota": "10.5",
		"unidad_medida": "7",
		"actualiza_precio":"S"
	},
	"leyenda": ""
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Los campos que debes enviar son los siguientes:

| `cantidad` | Campo numérico con 2 decimales. Separador de decimales: punto. **Ejemplo: 1.50** |
| :--- | :--- |
| `afecta_stock` | Campo alfanumérico de 1 posición. Valores posibles: "S" \(si\), "N" \(no\)  **Ejemplo: S** |
| `producto` | Según estructura de producto |
| `leyenda` | Campo alfanumérico. Longitud máxima 100 caracteres. Contenido opcional. Será una descripción que acompañe al producto.  **Ejemplo: Blanca, cepillada** |
| bonificacion\_porcentaje | Si se ha aplicado un porcentaje de descuento sobre éste concepto, debe ser enviado. Es un campo númerico con 2 decimales. El separador de decimales esperado es el punto. Ej:  25 |
|  |  |



### Estructura de "Concepto /  Producto"

{% hint style="info" %}
Si el producto ya existia en la base de datos de nuestra plataforma, para la lista de precios indicada, será actualizado con los nuevos datos.
{% endhint %}

```text
{
"descripcion":     "HUEVOS",
"unidad_bulto":    "30",
"lista_precios":   "MAPPLETS",
"codigo":          "MPH",
"precio_unitario_sin_iva":"50",
"alicuota":      "10.5",
"unidad_medida": "7",
"actualiza_precio": "N"
}
```

Los campos que debes enviar son los siguientes:

| `descripcion` | Campo alfanumérico. Longitud máxima 255 caracteres. **Ejemplo: Papa blanca** |
| :--- | :--- |
| `unidad_bulto` | Campo numérico entero requerido. Indica la cantidad de unidades que componen un bulto. Valor minimo esperado: 1 **Ejemplo: 12** |
| `lista_precios` | Campo alfanumérico. Longitud máxima 255 caracteres. Nombre de la lista de precios a la cual pertenece. No saldrá impreso en la factura pero es requerido. **Ejemplo: Verdura Orgánica** |
| `codigo` | Campo alfanumérico. Longitud máxima 10 caracteres. campo Opcional **Ejemplo: ABX780** |
| `precio_unitario_sin_iva` | Campo numérico con 2 decimales. separador de decimales: punto **Ejemplo: 645.67** |
| `alicuota` | Indica la alicuota de IVA con la que grava ese producto. Valores Permitidos: **27, 21 , 10.5 ,  0  y -1 \( para exento\)** **Ejemplo: 10.5** |
| `unidad_medida` | Campo numérico que indica la unidad de medida, según[ tabla de referencia Unidades de Medida\(\*\*\). ](../tablas-de-referencia.md#productos-unidades-de-medida-afip) **Ejemplo: 7** |
| `actualiza_precio` | Indica si se actualiza el precio del producto, en la base productos, tomando como valor de referencia el enviado en el comprobante. Campo Alfabético, de 1 caracter. Valores permitidos: S \(si\) N \(no\).          **Ejemplo: S** |
|  |  |

### Estructura de "Comprobantes Asociados"

Cada uno de los comprobantes asociados que disponga, deberán ser enviados dentro de un array, acorde a la estructura que se detalla a continuación para cada comprobante asociado.

{% hint style="info" %}
Solo se deberán enviar los comprobantes asociados, cuando se emitan Notas de Débito o Notas de Crédito de tipo A, B, C, M y Comprobantes de tipo FCE. **Éste campo es obligatorio en los campos mencionados.**
{% endhint %}

```text
 {
    "tipo_comprobante"   :    "FACTURA A",
     "punto_venta"  :    "145",
     "numero" : 12313,
     "comprobante_fecha": "07/07/2019",
     "cuit": 111111111     
} 
```

Información de los campos a enviar:

| `tipo_comprobante` | Campo alfabético. Valores esperados según [tabla de tipos de comprobante.](../tablas-de-referencia.md#tipos-de-comprobantes) |
| :--- | :--- |
| `punto_venta` | Campo numérico entero. Longitud máxima 5 digitos. **Ejemplo: 3** |
| `numero` | Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante. **Ejemplo: 4567** |
| `cuit` | Campo numérico, sin puntos ni guiones. Es el CUIT del emisor del comprobante asociado. **Ejemplo: 1111111111** |
| `comprobante_fecha` | La fecha del comprobante en formato dd/mm/aaaa |

### Estructura de "RG Especiales"

Según la RG a la que tu empresa aplique, se deberá enviar  un array con los datos adicionales, según se especifican en la [tabla de Datos adicionales para RG Especiales](../tablas-de-referencia.md#datos-opcionales-para-rg-especiales).

Ten en cuenta que solo podrás aplicar a un [regimen](../tablas-de-referencia.md#datos-opcionales-para-rg-especiales) por cada comprobante que emitas.

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
"rg_especiales":   
  {   "regimen" : "RG 4004-E",
      "datos"  : 
               [{
                   "id"      :    18,
                   "valor"  :    "PRUEBA "
                },
                {
                  "id"      :    19,
                 "valor"  :    "PRUEBA (2) "
                 }]
 } 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Información de los campos a enviar en el array de "datos":

| `id` | Campo númerico. Valores esperados según [ ](../tablas-de-referencia.md#tipos-de-comprobantes)[Tabla de Datos Opcionales para RG Especiales](../tablas-de-referencia.md#datos-opcionales-para-rg-especiales) |
| :--- | :--- |
| `valor` | Campo alfanumérico.  |

{% hint style="info" %}
Ten en cuenta que TusFacturas NO realiza validaciones sobre éstos campos. Los realiza la propia AFIP en caso que corresponda.

Si uno de los items enviados posee el valor vacio, éste item no será procesado.
{% endhint %}

## 

