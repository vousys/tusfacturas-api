---
description: >-
  Guía de referencia de errores comunes de ARCA en TusFacturasAPP: causas,
  soluciones rápidas y links a los artículos detallados de cada error.
icon: light-emergency-on
---

# Errores comunes de ARCA en TusFacturasAPP

ARCA puede devolver distintos tipos de errores al momento de facturar. Esta página reúne los más frecuentes, organizados por categoría, con una descripción breve de la causa y el link al artículo detallado con la solución paso a paso.

***

#### **Errores de certificado y enlace con ARCA**

Estos errores ocurren cuando el certificado digital que vincula tu cuenta con ARCA no está vigente, está mal configurado o el proceso de enlace no se completó correctamente.

| Error                                                      | Causa principal                                                                  | Solución                                                                                                                                   |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| No se puede establecer la comunicación con ARCA            | Certificado vencido o mal configurado                                            | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10355215-error-de-afip-no-se-puede-establecer-la-comunicacion-con-arca)           |
| Computador no autorizado                                   | El alias fue creado pero le faltan relaciones en ARCA                            | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10355512-error-de-afip-computador-no-autorizado)                                  |
| Java.null.pointer                                          | El archivo cargado en TusFacturasAPP no es compatible con ARCA                   | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10358967-error-afip-java-null-pointer)                                            |
| ValidacionDeToken: No apareció CUIT en lista de relaciones | El enlace se realizó con el CUIT de la persona física en lugar del de la empresa | [Ver solución](https://ayuda.tusfacturas.app/es/articles/15507777-error-de-arca-validaciondetoken-no-aparecio-cuit-en-lista-de-relaciones) |
| javax.ejb.EJBTransactionRolledbackException                | Error interno de ARCA, generalmente transitorio                                  | [Ver solución](https://ayuda.tusfacturas.app/es/articles/11542698-error-arca-javax-ejb-ejbtransactionrolledbackexception)                  |

***

#### **Errores de punto de venta**

Ocurren cuando el punto de venta no está correctamente configurado en ARCA o en TusFacturasAPP.

| Error                                                                                    | Causa principal                                                            | Solución                                                                                                                                                                             |
| ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| El punto de venta no se encuentra habilitado para el presente WS en AFIP                 | El PDV está configurado para "Comprobantes en línea" y no para webservices | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10355080-el-punto-de-venta-no-se-encuentra-habilitado-para-el-presente-ws-en-afip)                                          |
| No autorizado a emitir comprobantes – el PDV debe estar dado de alta y ser del tipo RECE | El PDV no está creado como RECE en ARCA                                    | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10497778-error-no-autorizado-a-emitir-comprobantes-el-punto-de-venta-informado-debe-estar-dado-de-alta-y-ser-del-tipo-rece) |
| Punto de venta no existe en Webservices ARCA pero lo veo en pantalla                     | El PDV fue creado en TusFacturasAPP pero no en ARCA o fue dado de baja     | [Ver solución](https://ayuda.tusfacturas.app/es/articles/12353006-error-punto-de-venta-no-existe-en-webservices-arca-pero-lo-veo-en-pantalla)                                        |

***

#### **Errores de numeración y fecha**

Ocurren cuando el número o la fecha del comprobante no coincide con lo que ARCA espera recibir.

| Error                                                                                                  | Causa principal                                                                            | Solución                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| El número o fecha del comprobante no se corresponde con el último a autorizar (FECompUltimoAutorizado) | La numeración en TusFacturasAPP y en ARCA están desincronizadas                            | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10453580-error-el-numero-o-fecha-del-comprobante-no-se-corresponde-con-el-ultimo-a-autorizar-consulte-el-metodo-fecompultimoautorizado) |
| Campo CbteFch debe estar comprendido en el rango N-10 y N+10                                           | La fecha del comprobante está fuera del rango permitido por ARCA                           | [Ver solución](https://ayuda.tusfacturas.app/es/articles/11463770-error-afip-campo-cbtefch-debe-estar-comprendido-en-el-rango-n-10-y-n-10-siendo-n-la-fecha-de-envio-del-pedido-de-autorizacion) |
| Error de numeración al facturar un abono                                                               | La numeración del abono se desincronizo de ARCA                                            | [Ver solución](https://ayuda.tusfacturas.app/es/articles/11905048-error-de-numeracion-al-facturar-un-abono)                                                                                      |
| El comprobante existe en ARCA pero no en TusFacturasAPP                                                | Caída de ARCA durante la emisión: el comprobante impactó en ARCA pero no en TusFacturasAPP | [Ver solución](https://ayuda.tusfacturas.app/es/articles/15574413-error-el-comprobante-existe-en-arca-pero-no-en-tusfacturasapp)                                                                 |

***

#### **Errores de comprobantes MiPyME (FCE)**

Específicos de Facturas de Crédito Electrónica MiPyME y sus notas de crédito/débito.

| Error                                                                                      | Causa principal                                                               | Solución                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| No es un comprobante válido bajo el Régimen de la Ley N° 27.440                            | El tipo de comprobante o el receptor no corresponde al régimen MiPyME         | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10355169-error-de-afip-no-es-un-comprobante-valido-bajo-el-regimen-de-la-ley-n-27-440)                                                                                            |
| Si informa comprobante MiPyMEs (FCE) del tipo Factura, es obligatorio informar opcional... | Faltan datos obligatorios del régimen FCE (CBU, tipo de transferencia)        | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10355175-error-de-afip-si-informa-comprobante-mipymes-fce-del-tipo-factura-es-obligatorio-informar-opcional)                                                                      |
| Campo CbtesAsoc con tipo inválido (NC/ND MiPyME)                                           | El tipo de comprobante asociado en la nota de crédito/débito no es correcto   | [Ver solución](https://ayuda.tusfacturas.app/es/articles/10546150-notas-de-credito-debito-mipyme-error-campo-cbtesasoc-con-tipo-invalido)                                                                                                  |
| El campo Condición IVA receptor no es válido para la clase de comprobante informado        | La condición IVA del receptor no es compatible con el tipo de nota de crédito | [Ver solución](https://ayuda.tusfacturas.app/es/articles/11498685-error-al-generar-una-nota-de-credito-el-campo-condicion-iva-receptor-no-es-valido-para-la-clase-de-comprobante-informado-consular-metodo-feparamgetcondicionivareceptor) |
| El comprobante asociado no posee una fecha válida                                          | La fecha del comprobante original que se intenta asociar está fuera de rango  | [Ver solución](https://ayuda.tusfacturas.app/es/articles/12801403-error-el-comprobante-asociado-xxxx-no-posee-una-fecha-valida)                                                                                                            |

***

#### **Errores de autorización de CUIT**

Ocurren cuando el CUIT no está habilitado para emitir determinados tipos de comprobantes.

| Error                                                                                                              | Causa principal                                                  | Solución                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| No autorizado a emitir comprobantes – la CUIT informada no se encuentra autorizada a emitir comprobantes clase "A" | El CUIT no tiene habilitada la emisión de comprobantes A en ARCA | [Ver solución](https://ayuda.tusfacturas.app/es/articles/13902064-error-de-arca-no-autorizado-a-emitir-comprobantes-la-cuit-informada-no-se-encuentra-autorizada-a-emitir-comprobantes-clase-a) |
| Validación de CUIT en ARCA: errores comunes                                                                        | El CUIT del receptor no pasa las validaciones de ARCA            | [Ver solución](https://ayuda.tusfacturas.app/es/articles/13570004-validacion-de-cuit-en-arca-errores-comunes)                                                                                   |

***

#### **Errores en comprobantes asociados**

Ocurren al emitir notas de crédito, notas de débito u otros comprobantes que referencian a uno anterior.

| Error                                                | Causa principal                                                      | Solución                                                                                                                                        |
| ---------------------------------------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Error AFIP/ARCA 10041                                | El comprobante asociado no existe o está mal referenciado            | [Ver solución](https://ayuda.tusfacturas.app/es/articles/11557313-error-afip-arca-10041)                                                        |
| Error ARCA 10041 - No existe el comprobante asociado | El comprobante al que se intenta asociar una NC/ND no figura en ARCA | [Ver solución](https://ayuda.tusfacturas.app/es/articles/11624427-error-arca-10041-no-existe-el-comprobante-asociado)                           |
| FchServDesde no puede ser posterior a FchServHasta   | Las fechas de servicio están invertidas en el comprobante            | [Ver solución](https://ayuda.tusfacturas.app/es/articles/13259511-solucion-al-error-fchservdesde-no-puede-ser-posterior-a-fchservhasta-de-arca) |

***

**¿No encontras tu error en esta lista?**

Contactate con nuestro [equipo de soporte](https://ayuda.tusfacturas.app/es/articles/12656184-conoce-nuestros-canales-oficiales) indicando el mensaje de error completo que ves en pantalla y el tipo de comprobante que intentabas emitir.
