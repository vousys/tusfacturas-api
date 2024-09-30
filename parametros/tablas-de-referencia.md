---
description: >-
  Integra tu sistema con la API Factura AFIP. Consulta las tablas de referencia
  para una facturación electrónica precisa y eficiente.
---

# Tablas de referencia

Obtené todos éstos datos haciendo un request a cada método, tomando como ejemplo el siguiente request:

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)`METODO`

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

| Name      | Type   | Description                |
| --------- | ------ | -------------------------- |
| apikey    | string | Tus credenciales de acceso |
| apitoken  | string | Tus credenciales de acceso |
| usertoken | string | Tus credenciales de acceso |

**Response**

{% tabs %}
{% tab title="JSON" %}
```json
{
    "apitoken":"TU_API_TOKEN",
    "apikey": 0101,
    "usertoken":"TU_USER_TOKEN"
}
```
{% endtab %}
{% endtabs %}



### Tipos de documento&#x20;

&#x20;Consulta todos los tipos de documento disponibles haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)documentos\_tipos

| Tipo de documento                   | Valor a enviar |
| ----------------------------------- | -------------- |
| DNI                                 | DNI            |
| CUIT                                | CUIT           |
| PASAPORTE                           | PASAPORTE      |
| OTRO (no requiere enviar el numero) | OTRO           |
| CDI                                 | CDI            |
| CUIL                                | CUIL           |
|                                     |                |

### Alícuotas de IVA

Consulta toda la información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)alicuotas\_iva

| Alicuota       | Valor a enviar |
| -------------- | -------------- |
| 27%            | 27             |
| 21%            | 21             |
| 10.5%          | 10.5           |
| 0%             | 0              |
| IVA Exento     | -1             |
| IVA No gravado | -2             |

### Provincias

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)provincias

| Provincia                       |   | Valor a enviar |
| ------------------------------- | - | -------------- |
| -                               |   | 26             |
| BUENOS AIRES                    |   | 2              |
| CATAMARCA                       |   | 3              |
| CHACO                           |   | 4              |
| CHUBUT                          |   | 5              |
| CIUDAD AUTONOMA DE BUENOS AIRES |   | 1              |
| CORDOBA                         |   | 6              |
| CORRIENTES                      |   | 7              |
| ENTRE RIOS                      |   | 8              |
| FORMOSA                         |   | 9              |
| JUJUY                           |   | 10             |
| LA PAMPA                        |   | 11             |
| LA RIOJA                        |   | 12             |
| MENDOZA                         |   | 13             |
| MISIONES                        |   | 14             |
| NEUQUEN                         |   | 15             |
| Otro                            |   | 25             |
| RIO NEGRO                       |   | 16             |
| SALTA                           |   | 17             |
| SAN JUAN                        |   | 18             |
| SAN LUIS                        |   | 19             |
| SANTA CRUZ                      |   | 20             |
| SANTA FE                        |   | 21             |
| SANTIAGO DEL ESTERO             |   | 22             |
| TIERRA DEL FUEGO                |   | 23             |
| TUCUMAN                         |   | 24             |

### Condiciones de venta

Consulta toda la información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)condiciones\_venta

| Condición de Venta               | Dias para vto comprobante (fecha fc) | Valor a enviar |
| -------------------------------- | ------------------------------------ | -------------- |
| 5 días                           | 5                                    | 213            |
| 10 dias                          | 10                                   | 206            |
| 15 dias                          | 15                                   | 207            |
| 20 dias                          | 20                                   | 209            |
| 30 dias                          | 30                                   | 202            |
| 45 dias                          | 45                                   | 208            |
| 60 dias                          | 60                                   | 203            |
| 90 dias                          | 90                                   | 204            |
| Contado                          | 0                                    | 201            |
| Cuenta corriente                 | 0                                    | 205            |
| Transferencia Bancaria           | 0                                    | 210            |
| Tarjeta de crédito               | 0                                    | 211            |
| Tarjeta de Débito                | 0                                    | 212            |
| Otra                             | 0                                    | 214            |
| Otros medios de pago electronico | 0                                    | 215            |

### Condiciones frente al IVA

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)condiciones\_iva

| Condición frente al IVA | Valor a enviar |
| ----------------------- | -------------- |
| Consumidor Final        | CF             |
| Responsable Inscripto   | RI             |
| Monotributo             | M              |
| Exento                  | E              |
| Cliente del exterior    | CDEX           |
| IVA No Alcanzado        | IVNA           |

### Tipos de comprobantes

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark>

&#x20;[`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)comprobantes\_tipos

| FACTURA A                                     |
| --------------------------------------------- |
| FACTURA B                                     |
| NOTA DE DEBITO A                              |
| NOTA DE DEBITO B                              |
| NOTA DE CREDITO A                             |
| NOTA DE CREDITO B                             |
| FACTURA NO VALIDA EN AFIP                     |
| NOTA DE CREDITO NO VALIDA EN AFIP             |
| FACTURA C                                     |
| NOTA DE DEBITO C                              |
| NOTA DE CREDITO C                             |
| FACTURA M                                     |
| NOTA DE DEBITO M                              |
| NOTA DE CREDITO M                             |
| FACTURA E                                     |
| NOTA DE DEBITO E                              |
| NOTA DE CREDITO E                             |
| RECIBO C                                      |
| FACTURA DE CREDITO ELECTRONICA MiPyME (FCE) A |
| NOTA DE DEBITO ELECTRONICA MiPyME (FCE) A     |
| NOTA DE CREDITO ELECTRONICA MiPyME (FCE) A    |
| FACTURA DE CREDITO ELECTRONICA MiPyME (FCE) B |
| NOTA DE DEBITO ELECTRONICA MiPyME (FCE) B     |
| NOTA DE CREDITO ELECTRONICA MiPyME (FCE) B    |
| FACTURA DE CREDITO ELECTRONICA MiPyME (FCE) C |
| NOTA DE DEBITO ELECTRONICA MiPyME (FCE) C     |
| NOTA DE CREDITO ELECTRONICA MiPyME (FCE) C    |

### Régimenes posibles para el bloque "RG\_Especiales"

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark>

[`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)rg\_especiales\_regimenes

| Regimen                                                           | id   | Descripcion                                                                               |
| ----------------------------------------------------------------- | ---- | ----------------------------------------------------------------------------------------- |
| RG Empresas Promovidas                                            | 2    | Indentificador de proyecto vinculado a Rógimen de Promoción Industrial                    |
| RG Bienes Usados 3411                                             | 91   | Nombre y Apellido o Denominación del vendedor del bien usado                              |
| RG Bienes Usados 3411                                             | 92   | Nacionalidad del vendedor del bien usado.                                                 |
| RG Bienes Usados 3411                                             | 93   | Domicilio del vendedor del bien usado                                                     |
| Excepcion computo IVA Credito Fiscal                              | 5    | Excepcion computo IVA Credito Fiscal                                                      |
| RG 3668 Impuesto al Valor Agregado                                | 61   | Art.12 IVA Firmante Doc Tipo                                                              |
| RG 3668 Impuesto al Valor Agregado                                | 62   | Art.12 IVA Firmante Doc Nro                                                               |
| RG 3668 Impuesto al Valor Agregado                                | 63   | Art.12 IVA Carócter del Firmante                                                          |
| RG 3.368 Establecimientos de educación pública de gestión privada | 10   | Actividad Comprendida                                                                     |
| RG 3.368 Establecimientos de educación pública de gestión privada | 1011 | Tipo de Documento                                                                         |
| RG 3.368 Establecimientos de educación pública de gestión privada | 1012 | Número de Documento                                                                       |
| RG 2.820 Operaciones económicas vinculadas con bienes inmuebles   | 11   | Actividad Comprendida                                                                     |
| RG 3.687 Locación temporaria de inmuebles con fines turísticos    | 12   | Actividad Comprendida                                                                     |
| RG 2.863 Representantes de Modelos                                | 13   | RG 2.863 Representantes de Modelos                                                        |
| RG 2.863 Agencias de publicidad                                   | 14   | RG 2.863 Agencias de publicidad                                                           |
| RG 2.863 Personas físicas que desarrollen actividad de modelaje   | 15   | RG 2.863 Personas físicas que desarrollen actividad de modelaje                           |
| RG 4004-E                                                         | 17   | Dato 2 (dos) = facturación directa / Dato 1 (uno) = facturación a travós de intermediario |
| RG 4004-E                                                         | 1801 | Clave ónica de Identificación Tributaria (CUIT)                                           |
| RG 4004-E                                                         | 1802 | Apellido y nombres, denominación y/o razón social                                         |
| Factura de Crédito Electrónica MiPyMEs (FCE)                      | 2101 | CBU del Emisor                                                                            |
| Factura de Crédito Electrónica MiPyMEs (FCE)                      | 2102 | Alias del Emisor                                                                          |
| Factura de Crédito Electrónica MiPyMEs (FCE)                      | 22   | Anulación                                                                                 |
| Factura de Crédito Electrónica MiPyMEs (FCE)                      | 23   | Referencia Comercial                                                                      |
| Factura de Crédito Electrónica MiPyMEs (FCE)                      | 27   | Referencia de transferencia                                                               |

### Monedas

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)monedas

| Moneda                  |   | Valor a enviar |
| ----------------------- | - | -------------- |
| Pesos Argentinos        |   | PES            |
| Dolares estadounidenses |   | DOL            |
| LIRAS ITALIANAS         |   | 004            |
| FRANCOS FRANCESES       |   | 003            |
| PESOS URUGUAYOS         |   | 011            |
| REAL                    |   | 012            |
| BOLIVAR (VENEZOLANO)    |   | 023            |
| PESO CHILENO            |   | 033            |
| PESO COLOMBIANO         |   | 032            |
| PESO BOLIVIANO          |   | 031            |
| EURO                    |   | 060            |
| SUCRE (ECUATORIANO)     |   | 036            |
| NUEVO SOL PERUANO       |   | 035            |
| PESOS MEJICANOS         |   | 010            |
|                         |   |                |

### Idiomas

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark> [`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)idiomas

| Idioma  |   | Valor a enviar |
| ------- | - | -------------- |
| Español |   | 1              |
| Ingles  |   | 2              |

### Productos - Unidades de Medida AFIP

{% hint style="info" %}
También puede consultar ésta información con el método [Consultar unidades de medida AFIP](https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#ejemplo-consultar-unidades-medida)
{% endhint %}

| Unidad de medida      |   | Valor a enviar |
| --------------------- | - | -------------- |
| 1000 kWh              |   | 6              |
| anulación/devolución  |   | 95             |
| centímetros           |   | 20             |
| cm cúbicos            |   | 27             |
| curie                 |   | 48             |
| dam cúbicos           |   | 30             |
| docenas               |   | 9              |
| gramo activo          |   | 67             |
| gramo base            |   | 68             |
| gramos                |   | 14             |
| gruesa                |   | 54             |
| hectolitros           |   | 18             |
| hm cúbicos            |   | 31             |
| jgo. pqt. mazo naipes |   | 25             |
| kg activo             |   | 66             |
| kg base               |   | 53             |
| kg bruto              |   | 61             |
| kilogramos            |   | 1              |
| kilómetros            |   | 17             |
| km cúbicos            |   | 32             |
| litros                |   | 5              |
| metros                |   | 2              |
| metros cuadrados      |   | 3              |
| metros cúbicos        |   | 4              |
| microcurie            |   | 50             |
| microgramos           |   | 33             |
| milicurie             |   | 49             |
| miligramos            |   | 41             |
| mililitros            |   | 47             |
| milimetros            |   | 15             |
| millares              |   | 11             |
| mm cúbicos            |   | 16             |
| muiactant             |   | 63             |
| muiacthor             |   | 52             |
| muiactig              |   | 65             |
| nanogramos            |   | 34             |
| otras unidades        |   | 98             |
| packs                 |   | 96             |
| pares                 |   | 8              |
| picogramos            |   | 35             |
| quilates              |   | 10             |
| seña/anticipo         |   | 97             |
| toneladas             |   | 29             |
| uiactant              |   | 62             |
| uiacthor              |   | 51             |
| uiactig               |   | 64             |
| unidades              |   | 7              |

### Bloque "tributos" :  Tipos de percepción a aplicar

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark>&#x20;

[`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)tributos\_percepciones\_tipos

| Si queres enviar..                   | Valor a enviar |
| ------------------------------------ | -------------- |
| Percepciones IVA                     | 6              |
| Percepciones IIBB                    | 7              |
| Percepciones de Impuestos Nacionales | 1              |

### Bloque "tributos" : Régimen de percepción

Consulta toda información disponible haciendo una petición a:&#x20;

<mark style="color:green;">`POST`</mark>&#x20;

[`https://www.tusfacturas.app/app/api/v2/tablas_referencia/`](https://www.tusfacturas.app/app/api/v2/tablas\_referencia/)tributos\_percepciones\_regimenes

| Tipo de tributo                      | Régimen                                | Valor a enviar |
| ------------------------------------ | -------------------------------------- | -------------- |
| Percepciones IVA                     | No especificado                        | 1              |
| Percepciones IVA                     | Reg. General (RG 2408)                 | 2              |
| Percepciones IVA                     | RG 5329                                | 3              |
| Percepciones IIBB                    | CAPITAL FEDERAL                        | 4              |
| Percepciones IIBB                    | BUENOS AIRES                           | 5              |
| Percepciones IIBB                    | CATAMARCA                              | 6              |
| Percepciones IIBB                    | CHACO                                  | 7              |
| Percepciones IIBB                    | CHUBUT                                 | 8              |
| Percepciones IIBB                    | CORDOBA                                | 9              |
| Percepciones IIBB                    | CORRIENTES                             | 10             |
| Percepciones IIBB                    | ENTRE RIOS                             | 11             |
| Percepciones IIBB                    | FORMOSA                                | 12             |
| Percepciones IIBB                    | JUJUY                                  | 13             |
| Percepciones IIBB                    | LA PAMPA                               | 14             |
| Percepciones IIBB                    | LA RIOJA                               | 15             |
| Percepciones IIBB                    | MENDOZA                                | 16             |
| Percepciones IIBB                    | MISIONES                               | 17             |
| Percepciones IIBB                    | NEUQUEN                                | 18             |
| Percepciones IIBB                    | RIO NEGRO                              | 19             |
| Percepciones IIBB                    | SALTA                                  | 20             |
| Percepciones IIBB                    | SAN JUAN                               | 21             |
| Percepciones IIBB                    | SAN LUIS                               | 22             |
| Percepciones IIBB                    | SANTA CRUZ                             | 23             |
| Percepciones IIBB                    | SANTA FE                               | 24             |
| Percepciones IIBB                    | SANTIAGO DEL ESTERO                    | 25             |
| Percepciones IIBB                    | TIERRA DEL FUEGO                       | 26             |
| Percepciones IIBB                    | TUCUMAN                                | 27             |
| Percepciones IIBB                    | Otro                                   | 28             |
| Percepciones de Impuestos Nacionales | Perc. impuesto PAIS                    | 31             |
| Percepciones de Impuestos Nacionales | Impuesto Pais                          | 32             |
| Percepciones de Impuestos Nacionales | Perc. Imp. a las Ganancias             | 33             |
| Percepciones de Impuestos Nacionales | Perc. Imp. sobre los Bienes Personales | 34             |
|                                      |                                        |                |



