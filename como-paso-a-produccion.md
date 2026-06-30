---
description: >-
  API de facturación electrónica ARCA: Cómo pasar a Producción: Recomendaciones
  y Pasos a Seguir
---

# 🚀 ¿Cómo paso a producción?

Una vez completadas las pruebas con tu **Plan API DEV**, es momento de migrar tu integración a producción para comenzar a emitir facturas electrónicas con validez legal. Esta guía te acompañará paso a paso en el proceso de transición.

***

### 📋 Antes de Comenzar: Checklist de Preparación

Antes de iniciar el proceso de migración, asegurate de haber completado:

* ✅ **Pruebas exhaustivas** de tu integración
* ✅ **Validación** de todos los tipos de comprobantes que necesitás
* ✅ **Verificación** de los flujos de error y manejo de excepciones
* ✅ **Documentación** de tu integración para futuro mantenimiento
* ✅ **Backup** de tu código y configuraciones de desarrollo

***

### 🔄 Opciones para tu estrategias de Migración:&#x20;

#### Opción 1: Crear Nueva Cuenta para tu integración (Recomendada)

**✅ Ventajas:**

* Entorno completamente limpio
* Conservás tu cuenta de desarrollo para futuras pruebas
* Ideal para cuentas de clientes separadas

**⚠️ Consideraciones:**

* Requiere una configuración completa de tu cuenta&#x20;

#### Opción 2: Reutilizar Cuenta de Desarrollo&#x20;

**✅ Ventajas:**

* Mantenés toda tu configuración actual
* Conservás el historial de desarrollo
* Proceso más rápido

**⚠️ Consideraciones:**

* Debés limpiar los datos de prueba antes de la migración
* Una vez vinculado con AFIP/ARCA, no podrás usar planes API DEV en esta cuenta

{% hint style="info" %}
Conoce la guía que datos necesitas pedirle a tus clientes para hacer el onboarding en TusFacturasAPP

<a href="https://ayuda.tusfacturas.app/es/articles/15706757-que-informacion-necesito-pedirle-a-mis-usuarios-para-integrarlos-con-la-api-de-tusfacturasapp" class="button primary" data-icon="rocket-launch">Requisitos de Onboarding para clientes</a>
{% endhint %}

***

### 🛠️ Proceso de Migración Paso a Paso

{% stepper %}
{% step %}
#### Paso 1: Preparación de la Cuenta

**Si reutilizás tu cuenta de desarrollo:**

1. **Eliminá los comprobantes de prueba:**
   * Accedé a  [TusFacturasAPP](https://www.tusfacturas.app/) e ingresá a tu cuenta.
   * Navegá a **Menú > Facturación > Mis ventas**
   * Eliminá todos los comprobantes asociados al CUIT/PDV de prueba
   * Verificá que no queden registros de desarrollo
2. **Limpiá configuraciones de prueba:**
   * Revisá los productos y servicios de prueba
   * Eliminá clientes ficticios
   * Verificá las configuraciones de puntos de venta

**Si creás una nueva cuenta:**

1. **Registrá la nueva cuenta** en [TusFacturasAPP](https://www.tusfacturas.app/registrarme-factura-electronica.html)
2. **Accedé a:** Menú > Mi espacio de trabajo > Puntos de venta > Crear nuevo
3. **Configurá los datos reales** del punto de venta:
   * CUIT real de tu cliente/empresa
   * Punto de venta oficial asignado por AFIP/ARCA
   * Razón social correcta
   * Domicilio fiscal
{% endstep %}

{% step %}
#### Paso 2: Contratación del Plan API de Producción

1. **Accedé a la plataforma web**
2. **Navegá a:** Menú > Mi cuenta > Cambiar o renovar mi plan actual
3. **Consultá los** [**planes API disponibles**](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html)
4. **Seleccioná el plan** que mejor se adapte a tu volumen de facturación

#### **💡 Gestión de Transición de Planes**

**Si tu Plan API DEV está activo:**

* La nueva suscripción comenzará cuando expire la actual
* Para activar inmediatamente, contactá a [soporte@tusfacturas.app](mailto:soporte@tusfacturas.app)
* O [activá manualmente](https://ayuda.tusfacturas.app/es/articles/10354324-me-quede-sin-cupo-como-activo-mi-nueva-suscripcion-a-partir-de-hoy) desde **Menú > Mi cuenta > Mis suscripciones**
{% endstep %}

{% step %}
#### Paso 3: Vincula tu cuenta de TusFacturasAPP con AFIP/ARCA

**📧 Certificado Digital**

Después de crear el punto de venta, recibirás un **email con un certificado** para realizar la vinculación con AFIP/ARCA.

**🔗 Proceso de Enlace**

1. **Seguí nuestro** [**instructivo interactivo de enlace ARCA**](https://www.tusfacturas.app/enlace-arca.html)
2. **Completá la vinculación** siguiendo cada paso cuidadosamente
3. **Verificá que la conexión** se haya establecido correctamente
{% endstep %}

{% step %}
#### Paso 4: Sincronización de Numeración

Una vez completada la vinculación con AFIP/ARCA:

1. **Accedé a:** Menú > Facturación > Recuperar numeración desde AFIP/ARCA
2. **Ejecutá la sincronización** para actualizar el numerador interno
3. **Verificá que la numeración** coincida con la oficial de AFIP/ARCA

⚠️ **Importante:** Este proceso se ejecuta **una única vez** y asegura que tu configuración esté lista para producción.
{% endstep %}
{% endstepper %}

***

### 🔧 Actualización de Credenciales API

#### Nuevas Credenciales de Producción

Una vez completada la migración, necesitarás actualizar las credenciales en tu aplicación:

```json
{
  "apitoken": "nuevo_token_produccion",
  "apikey": "nueva_key_produccion", 
  "usertoken": "nuevo_user_token_produccion"
}
```

#### 📍 Dónde Encontrar las Credenciales

* **Ubicación:** Menú > Mi espacio de trabajo > Puntos de venta
* **Seleccioná** el punto de venta de producción
* **Copiá** las nuevas credenciales

#### 🔄 Actualización en tu Código

Asegurate de actualizar **todas las referencias** a las credenciales en:

* Variables de entorno
* Archivos de configuración
* Código de la aplicación
* Documentación del equipo

***

### 🧪 Pruebas de Producción

#### Checklist de Validación

Antes de lanzar completamente, realizá estas verificaciones:

* ✅ **Emitir una factura de prueba** con datos reales
* ✅ **Verificar la numeración** en AFIP/ARCA
* ✅ **Comprobar la recepción** del comprobante por email
* ✅ **Validar el PDF generado** y su formato
* ✅ **Revisar los campos CAE** y fecha de vencimiento
* ✅ **Probar diferentes tipos** de comprobantes (A, B, C)
* ✅ **Verificar el manejo de errores** en producción

#### 📊 Monitoreo Inicial

Durante los primeros días en producción:

* Supervisá el volumen de facturas emitidas
* Verificá la estabilidad de la integración
* Monitoreá los tiempos de respuesta
* Revisá los logs de errores

***

### 🚨 Consideraciones Importantes

#### ⚠️ Puntos Críticos

1. **Una vez vinculado con AFIP/ARCA**, no podrás volver a usar planes API DEV en esa cuenta
2. **Los comprobantes emitidos en producción** tienen validez legal y son irrevocables
3. **La numeración debe ser consecutiva** según las normativas AFIP/ARCA
4. **Mantené siempre un backup** de tu configuración de producción

#### 🔒 Seguridad

* **Protegé las credenciales** de producción
* **Usá HTTPS** en todas las comunicaciones
* **Implementá logs** de auditoria
* **Configurá alertas** para errores críticos

***

### 📈 Escalabilidad y Planes

Si necesitás cambiar tu plan:

* Podés **escalar hacia arriba** en cualquier momento
* Los cambios se reflejan en el próximo ciclo de facturación
* Contactá a soporte para cambios inmediatos

***

### 🆘 Soporte y Asistencia

#### 📞 Canales de Soporte

* **📧 Email:** api@tusfacturas.app
* **💬 Chat:** Disponible en [www.tusfacturas.app](https://www.tusfacturas.app/)
* :information\_source: Centro de Ayuda: [https://ayuda.tusfacturas.app/es](https://ayuda.tusfacturas.app/es)

#### 🕐 Horarios de Atención personalizada

* **Lunes a Viernes:** 9:00 - 15:30 (GMT-3)

#### 📚 Recursos Adicionales

* [**Centro de Ayuda**](https://ayuda.tusfacturas.app/es/)
* [**Documentación API completa**](api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md)
* [**Ejemplos de código**](web-services-afip-api-arca/)
* [**Status de servicios**](https://www.tusfacturas.app/app/estado-servicios.html)

***

### 🚀 ¡Listo para Producción!

Siguiendo esta guía, garantizarás una transición ordenada y sin registros de prueba en tu entorno de producción. Tu integración estará lista para emitir facturas electrónicas AFIP/ARCA con total validez legal.

¿Necesitás asistencia durante el proceso? Nuestro equipo de soporte está disponible para ayudarte en cada paso.

[**🎯 Comenzar migración ahora**](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html)

