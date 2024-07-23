---
description: >-
  Consulta desde la API de  TusFacturas.app, la cuenta corriente de tus
  clientes.
---

# Consulta de Cuentas Corrientes

## Consulta de cuenta corriente

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/apiv2/`<mark style="color:purple;">`clientes/cuenta-corriente`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción

#### Request Body

| Name      | Type   | Description                                                                 |
| --------- | ------ | --------------------------------------------------------------------------- |
| cliente   | object | <p><strong>documento_tipo</strong></p><p><strong>documento_nro</strong></p> |
| usertoken | string | Tus credenciales de acceso                                                  |
| apikey    | string | Tus credenciales de acceso                                                  |
| apitoken  | string | Tus credenciales de acceso                                                  |

### Ejemplo del JSON que debes enviar

```
{
    "usertoken" :  "xxxx",
    "apikey"    :  "xxxx",    
    "apitoken"  :  "xxxx",    
    "cliente":  {       
      "documento_nro":    "30712293841",
      "documento_tipo":   "CUIT"
      }
  }
```

### Estructura de "Cliente"

| `documento_tipo` | <p>Valores Permitidos: <strong>CUIT</strong><br><strong>Ejemplo: CUIT</strong></p>     |
| ---------------- | -------------------------------------------------------------------------------------- |
| `documento_nro`  | <p>Campo numérico, sin puntos ni guiones.<br><strong>Ejemplo: 30111222334</strong></p> |

### Estructura de los datos devueltos

Se devolverá una lista, conteniendo la siguiente estructura, con cada uno de los registros de la cuenta corriente de tu cliente.

```
    {
        "fecha":"11\/05\/2017",
        "concepto":"FACTURA A 0002-00000002 (CUIT DE PRUEBA)",
        "debe":112.1,
        "haber":0,
        "resta_abonar_de_este_comprobante":112.1,
        "saldo":224.2
    }
```
