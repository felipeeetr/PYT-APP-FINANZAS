# FinTrack — Documento de Requisitos

**Versión:** 1.0
**Estado:** Borrador para revisión
**Proyecto:** FinTrack
**Tipo:** Aplicación móvil multiplataforma de gestión financiera personal
**Idioma inicial:** Español
**Moneda inicial:** Peso colombiano (COP)

---

# 1. Descripción general

## 1.1 Propósito

FinTrack es una aplicación móvil de gestión financiera personal cuyo objetivo es permitir al usuario registrar, organizar, consultar y analizar sus finanzas personales desde un único lugar.

La aplicación permitirá administrar cuentas bancarias, efectivo, movimientos financieros, tarjetas de crédito, préstamos, presupuestos, metas de ahorro y compromisos recurrentes.

Además, proporcionará un dashboard visual con información financiera relevante, gráficos, calendarios, notificaciones y generación de reportes.

El sistema deberá estar diseñado para que la información financiera de cada usuario permanezca completamente aislada de la información de otros usuarios.

---

# 2. Alcance del proyecto

## 2.1 Alcance inicial

La primera versión de FinTrack deberá contemplar:

* Registro e inicio de sesión.
* Gestión de perfiles.
* Autenticación segura.
* Gestión de cuentas bancarias y efectivo.
* Registro de ingresos.
* Registro de gastos.
* Transferencias entre cuentas.
* Manejo de efectivo.
* Gestión de tarjetas de crédito.
* Compras a cuotas.
* Gestión básica de préstamos.
* Gestión de categorías.
* Presupuestos.
* Compromisos y gastos recurrentes.
* Metas de ahorro.
* Dashboard financiero.
* Análisis mediante gráficos.
* Calendario financiero.
* Notificaciones.
* Reportes.
* Exportación de información.
* Funcionamiento parcial sin conexión.
* Sincronización posterior.
* Preparación de los datos para análisis posterior en Power BI.

## 2.2 Funciones inicialmente fuera del alcance

Las siguientes funcionalidades podrán incorporarse posteriormente:

* Cuentas compartidas o familiares.
* Integración directa con bancos.
* Importación automática de movimientos bancarios.
* Múltiples monedas.
* Funciones avanzadas de inteligencia artificial.
* Widget de pantalla de inicio.
* Integraciones financieras externas.
* Cálculos avanzados de intereses de tarjetas.
* Gestión avanzada de cuotas y cargos financieros.
* Integración avanzada y directa con Power BI.
* Subcategorías.
* Funciones financieras empresariales.

---

# 3. Usuarios y aislamiento de información

## 3.1 Usuarios

FinTrack estará diseñado inicialmente para usuarios independientes.

Cada usuario tendrá su propia información financiera.

No se implementarán inicialmente cuentas familiares, cuentas compartidas ni roles administrativos para compartir información financiera.

## 3.2 Aislamiento de información

El sistema deberá garantizar que:

* Un usuario solamente pueda consultar sus propios datos.
* Un usuario solamente pueda modificar sus propios datos.
* Un usuario solamente pueda eliminar sus propios datos.
* Las cuentas, movimientos, tarjetas, préstamos, metas y demás elementos financieros estén asociados al usuario correspondiente.

---

# 4. Autenticación y seguridad

## RF-AUTH-001 — Registro

El sistema deberá permitir al usuario crear una cuenta proporcionando la información necesaria para su identificación y autenticación.

## RF-AUTH-002 — Inicio de sesión

El sistema deberá permitir al usuario iniciar sesión mediante sus credenciales.

## RF-AUTH-003 — Cierre de sesión

El sistema deberá permitir cerrar la sesión actual.

## RF-AUTH-004 — Recuperación de contraseña

El sistema deberá permitir recuperar una contraseña olvidada mediante un mecanismo seguro.

## RF-AUTH-005 — Cambio de contraseña

El usuario deberá poder cambiar su contraseña desde su perfil.

## RF-AUTH-006 — Sesión persistente

El sistema deberá permitir mantener la sesión iniciada de forma segura para evitar solicitar las credenciales en cada apertura de la aplicación.

## RF-AUTH-007 — Autenticación mediante token

Las operaciones protegidas deberán requerir autenticación mediante un mecanismo basado en tokens.

## RF-AUTH-008 — Inicio de sesión desde un nuevo dispositivo

Cuando el usuario inicie sesión desde un dispositivo nuevo, el sistema podrá solicitar:

1. Correo electrónico.
2. Contraseña.
3. Código de verificación enviado al correo.

## RF-AUTH-009 — Protección de operaciones sensibles

Las operaciones consideradas sensibles deberán requerir una nueva confirmación de identidad.

Entre ellas:

* Eliminación permanente de información financiera.
* Desactivación o eliminación de cuentas.
* Operaciones destructivas importantes.
* Otras operaciones que posteriormente sean clasificadas como sensibles.

## RF-AUTH-010 — Biometría

El sistema podrá permitir autenticación mediante mecanismos biométricos disponibles en el dispositivo, como huella digital o reconocimiento facial.

Esta funcionalidad deberá implementarse de manera segura y dependerá de las capacidades del dispositivo.

---

# 5. Perfil del usuario

## RF-PROFILE-001 — Visualización del perfil

El usuario deberá poder consultar su información personal registrada.

## RF-PROFILE-002 — Edición del perfil

El usuario deberá poder modificar la información permitida de su perfil.

## RF-PROFILE-003 — Configuración de seguridad

El usuario deberá poder administrar las opciones de seguridad disponibles.

---

# 6. Gestión de cuentas financieras

Las cuentas representan los lugares donde el usuario mantiene dinero disponible.

Inicialmente se contemplarán:

* Cuentas bancarias.
* Efectivo.

Otros medios digitales podrán representarse conceptualmente como cuentas financieras sin necesidad de crear una categoría arquitectónica independiente.

## RF-ACCOUNT-001 — Crear cuenta

El sistema deberá permitir crear una cuenta financiera.

La cuenta podrá contener información como:

* Nombre.
* Tipo.
* Institución, cuando corresponda.
* Saldo inicial.
* Estado.
* Información adicional.

## RF-ACCOUNT-002 — Consultar cuentas

El usuario deberá poder consultar todas sus cuentas.

## RF-ACCOUNT-003 — Consultar saldo

El sistema deberá mostrar el saldo disponible de cada cuenta.

## RF-ACCOUNT-004 — Editar cuenta

El usuario deberá poder modificar la información de una cuenta.

## RF-ACCOUNT-005 — Desactivar cuenta

El usuario deberá poder desactivar una cuenta sin perder necesariamente su historial.

## RF-ACCOUNT-006 — Historial de cuenta

El usuario deberá poder consultar los movimientos relacionados con una cuenta.

## RF-ACCOUNT-007 — Eliminación de cuenta

El sistema podrá permitir la eliminación permanente de una cuenta bajo condiciones de seguridad.

Antes de realizar una eliminación permanente, el sistema deberá advertir al usuario sobre las consecuencias.

## RF-ACCOUNT-008 — Preservación del historial

El sistema deberá contemplar mecanismos para conservar información histórica cuando una cuenta sea desactivada.

---

# 7. Movimientos financieros

Los movimientos financieros iniciales serán:

* Ingreso.
* Gasto.
* Transferencia.

## RF-TRANSACTION-001 — Registrar ingreso

El sistema deberá permitir registrar un ingreso indicando como mínimo:

* Valor.
* Fecha.
* Categoría.
* Cuenta de destino.
* Descripción opcional.

## RF-TRANSACTION-002 — Registrar gasto

El sistema deberá permitir registrar un gasto indicando como mínimo:

* Valor.
* Fecha.
* Categoría.
* Medio de pago.
* Descripción opcional.

## RF-TRANSACTION-003 — Registrar transferencia

El sistema deberá permitir transferir dinero entre cuentas pertenecientes al mismo usuario.

## RF-TRANSACTION-004 — Editar movimiento

El usuario deberá poder modificar un movimiento registrado.

## RF-TRANSACTION-005 — Eliminar movimiento

El usuario deberá poder eliminar un movimiento bajo las condiciones de seguridad definidas por el sistema.

## RF-TRANSACTION-006 — Anular movimiento

El sistema deberá permitir anular determinados movimientos sin eliminar completamente su registro histórico.

## RF-TRANSACTION-007 — Historial

El sistema deberá permitir consultar el historial de movimientos.

## RF-TRANSACTION-008 — Filtrar movimientos

El usuario deberá poder filtrar movimientos mediante un selector de rango de fechas.

Se podrán proporcionar rangos rápidos como:

* Hoy.
* Esta semana.
* Últimas dos semanas.
* Últimas cuatro semanas.
* Este mes.
* Mes anterior.
* Últimos tres meses.
* Año.
* Rango personalizado.

---

# 8. Medios de pago

Al registrar un gasto, el usuario deberá poder indicar el medio utilizado.

Inicialmente se contemplarán:

* Efectivo.
* Cuenta bancaria.
* Otra cuenta financiera.
* Tarjeta de crédito.

El sistema deberá diferenciar correctamente entre el medio utilizado para realizar una compra y el impacto financiero real de la operación.

---

# 9. Transferencias y efectivo

## RF-TRANSFER-001 — Transferencia entre cuentas

El usuario deberá poder mover dinero de una cuenta propia hacia otra cuenta propia.

Visualmente, el sistema podrá mostrar la operación como una única transferencia.

Internamente deberá poder representar:

```text
Cuenta origen: -$300.000
Cuenta destino: +$300.000
```

## RF-CASH-001 — Retiro de efectivo

El sistema deberá permitir retirar dinero de una cuenta y registrarlo como efectivo.

Ejemplo:

```text
Bancolombia: -$300.000
Efectivo: +$300.000
```

La operación no deberá considerarse un gasto.

## RF-CASH-002 — Gasto con efectivo

Posteriormente, el usuario podrá registrar:

```text
Efectivo: -$50.000
Gasto: $50.000
```

Este movimiento sí deberá afectar las estadísticas de gastos.

---

# 10. Reembolsos y anulaciones

## RF-TRANSACTION-009 — Corrección de gasto

El usuario deberá poder modificar un gasto cuando se haya registrado incorrectamente.

## RF-TRANSACTION-010 — Anulación

El usuario deberá poder anular determinados movimientos.

Un movimiento anulado deberá permanecer identificable en el historial y dejar de afectar los cálculos financieros correspondientes.

El movimiento podrá visualizarse con un estado como:

**ANULADO**

---

# 11. Tarjetas de crédito

Las tarjetas de crédito serán entidades independientes de las cuentas normales.

## RF-CARD-001 — Registrar tarjeta

El usuario deberá poder registrar una tarjeta de crédito.

La información podrá incluir:

* Nombre.
* Límite de crédito.
* Deuda actual.
* Crédito disponible.
* Fecha de corte.
* Fecha límite de pago.
* Configuración de cargos administrativos.
* Información adicional.

## RF-CARD-002 — Consultar deuda

El sistema deberá mostrar la deuda actual de la tarjeta.

## RF-CARD-003 — Consultar crédito disponible

El sistema deberá mostrar el crédito disponible.

## RF-CARD-004 — Registrar compra con tarjeta

El usuario deberá poder registrar una compra realizada mediante tarjeta de crédito.

La compra deberá incrementar la deuda de la tarjeta y no deberá descontarse inmediatamente de una cuenta bancaria.

## RF-CARD-005 — Compra a cuotas

El usuario deberá poder registrar una compra indicando el número de cuotas.

## RF-CARD-006 — Generar cuotas

El sistema deberá generar las cuotas correspondientes a la compra y asociarlas con la compra original.

## RF-CARD-007 — Consultar cuotas

El usuario deberá poder consultar:

* Cuotas pagadas.
* Cuotas pendientes.
* Próximas cuotas.
* Valor de cada cuota.
* Fecha correspondiente.

## RF-CARD-008 — Pagos parciales

El sistema deberá permitir registrar pagos parciales de una deuda.

Deberá mostrar claramente el valor restante.

## RF-CARD-009 — Pago de tarjeta

El usuario deberá poder registrar el pago de una tarjeta seleccionando la cuenta desde la cual se realizará el pago.

El pago deberá:

* Disminuir la deuda de la tarjeta.
* Disminuir el saldo de la cuenta utilizada.
* No registrarse como un gasto ordinario.

## RF-CARD-010 — Calendario de pagos

El sistema deberá mostrar las obligaciones futuras relacionadas con tarjetas.

## RF-CARD-011 — Fechas configurables

Las fechas de corte y pago deberán utilizarse automáticamente para organizar las obligaciones, pero el usuario deberá poder modificarlas cuando sea necesario.

## RF-CARD-012 — Detalles de tarjeta

La pantalla de tarjeta deberá mostrar información resumida y permitir acceder a una sección de detalles.

## RF-CARD-013 — Intereses y cargos avanzados

La gestión avanzada de intereses y cargos administrativos se considerará una funcionalidad posterior y deberá implementarse únicamente después de definir correctamente las reglas financieras correspondientes.

---

# 12. Préstamos

FinTrack deberá permitir gestionar tanto dinero recibido como dinero prestado a terceros.

## RF-LOAN-001 — Registrar préstamo recibido

El usuario deberá poder registrar dinero recibido como préstamo.

El sistema deberá registrar:

* Valor recibido.
* Acreedor.
* Fecha.
* Condiciones.
* Información de pago.

El dinero recibido deberá aumentar el dinero disponible y generar una obligación de deuda.

## RF-LOAN-002 — Registrar préstamo otorgado

El usuario deberá poder registrar dinero prestado a otra persona.

El sistema deberá registrar el valor que el tercero debe devolver.

## RF-LOAN-003 — Configurar pago

El usuario deberá poder definir:

* Fecha de vencimiento.
* Pago único.
* Número de cuotas.
* Fechas de pago.
* Valores correspondientes.

## RF-LOAN-004 — Registrar pago de préstamo

El sistema deberá permitir registrar el pago de una obligación.

La operación deberá reducir:

* El saldo de la cuenta utilizada.
* La deuda correspondiente.

## RF-LOAN-005 — Calendario de préstamos

Los pagos de préstamos deberán aparecer en el calendario financiero.

## RF-LOAN-006 — Notificaciones

El sistema deberá poder notificar al usuario sobre próximos vencimientos de préstamos.

---

# 13. Categorías

## RF-CATEGORY-001 — Categorías predeterminadas

El sistema deberá proporcionar inicialmente categorías como:

* Alimentación.
* Transporte.
* Vivienda.
* Entretenimiento.
* Salud.
* Educación.
* Trabajo.
* Compras.
* Tecnología.
* Otros.

## RF-CATEGORY-002 — Crear categoría

El usuario deberá poder crear categorías personalizadas.

## RF-CATEGORY-003 — Editar categoría

El usuario deberá poder modificar categorías.

## RF-CATEGORY-004 — Eliminar o desactivar categoría

El usuario deberá poder eliminar o desactivar categorías cuando no existan restricciones relacionadas con movimientos históricos.

## RF-CATEGORY-005 — Personalización

El usuario podrá modificar las categorías predeterminadas.

## RF-CATEGORY-006 — Subcategorías

Las subcategorías no formarán parte de la primera versión.

---

# 14. Presupuestos

## RF-BUDGET-001 — Crear presupuesto

El usuario deberá poder crear un presupuesto asociado a una categoría.

## RF-BUDGET-002 — Definir límite

El usuario deberá establecer el valor máximo que desea presupuestar para una categoría durante un período.

## RF-BUDGET-003 — Consultar progreso

El sistema deberá mostrar:

* Valor presupuestado.
* Valor gastado.
* Porcentaje utilizado.
* Valor restante.

Ejemplo:

```text
Alimentación
Presupuesto: $500.000
Gastado: $340.000
Progreso: 68%
Disponible: $160.000
```

## RF-BUDGET-004 — Alertas

El sistema deberá generar alertas cuando el usuario se encuentre cerca del límite definido.

## RF-BUDGET-005 — Presupuesto excedido

Cuando el usuario supere el presupuesto, el sistema deberá mostrar una alerta y una indicación visual.

El presupuesto no deberá bloquear al usuario de realizar nuevos gastos.

---

# 15. Compromisos y gastos recurrentes

FinTrack deberá permitir registrar obligaciones que ocurren periódicamente.

Ejemplos:

* Arriendo.
* Internet.
* Telefonía.
* Suscripciones.
* Servicios.
* Otros compromisos verdaderamente recurrentes.

## RF-RECURRING-001 — Crear compromiso recurrente

El usuario deberá poder definir:

* Nombre.
* Valor habitual.
* Frecuencia.
* Fecha.
* Categoría.
* Cuenta o medio de pago.
* Información adicional.

## RF-RECURRING-002 — Generar próximo compromiso

El sistema deberá preparar o generar el próximo movimiento correspondiente.

El usuario podrá confirmar o modificar el movimiento.

## RF-RECURRING-003 — Cambio de valor

Cuando el valor de una obligación recurrente cambie, el sistema deberá permitir identificar si:

* El cambio aplica únicamente a esa ocurrencia.
* El nuevo valor debe mantenerse para futuras ocurrencias.

## RF-RECURRING-004 — Recordatorios

El sistema deberá poder notificar al usuario sobre compromisos próximos.

---

# 16. Metas de ahorro

## RF-GOAL-001 — Crear meta

El usuario deberá poder crear una meta financiera.

La meta podrá contener:

* Nombre.
* Valor objetivo.
* Fecha objetivo opcional.
* Cuenta asociada o apartado independiente.
* Descripción.

## RF-GOAL-002 — Contribuciones

El usuario podrá realizar contribuciones a una meta.

La contribución podrá ser:

* Mayor a la recomendada.
* Menor a la recomendada.
* Igual a la recomendada.
* Cero durante un período.

## RF-GOAL-003 — Recomendación de aporte

Cuando exista una fecha objetivo, el sistema podrá calcular un aporte recomendado para alcanzar la meta.

El valor recomendado será informativo y no obligará al usuario a realizar dicho aporte.

## RF-GOAL-004 — Historial

El sistema deberá registrar las contribuciones realizadas y su procedencia.

## RF-GOAL-005 — Retiro

El usuario podrá retirar dinero de una meta.

El sistema deberá registrar dicho retiro.

## RF-GOAL-006 — Progreso

El sistema deberá mostrar:

* Valor acumulado.
* Valor restante.
* Porcentaje de progreso.
* Fecha objetivo, cuando exista.
* Aporte recomendado, cuando corresponda.

---

# 17. Dashboard financiero

El dashboard será la pantalla principal de análisis de la situación financiera.

## RF-DASHBOARD-001 — Dinero disponible

El sistema deberá mostrar el dinero actualmente disponible.

## RF-DASHBOARD-002 — Patrimonio neto

El sistema deberá calcular y mostrar el patrimonio neto de acuerdo con la información registrada.

## RF-DASHBOARD-003 — Ingresos

El sistema deberá mostrar los ingresos correspondientes al período seleccionado.

## RF-DASHBOARD-004 — Gastos

El sistema deberá mostrar los gastos correspondientes al período seleccionado.

## RF-DASHBOARD-005 — Ahorro

El sistema deberá mostrar información relacionada con el ahorro del período.

## RF-DASHBOARD-006 — Distribución del dinero

El sistema deberá mostrar cómo está distribuido el dinero entre las diferentes cuentas.

## RF-DASHBOARD-007 — Deuda

El dashboard deberá mostrar información relacionada con las obligaciones financieras.

Podrá incluir:

* Deuda de tarjetas.
* Préstamos.
* Otras obligaciones registradas.

## RF-DASHBOARD-008 — Categorías

El sistema deberá mostrar información sobre la distribución de gastos por categoría.

## RF-DASHBOARD-009 — Presupuestos

El dashboard deberá mostrar el progreso de los presupuestos relevantes.

## RF-DASHBOARD-010 — Metas

El dashboard deberá mostrar el progreso de las metas activas.

## RF-DASHBOARD-011 — Próximos pagos

El sistema deberá mostrar próximas obligaciones financieras.

## RF-DASHBOARD-012 — Movimientos recientes

El dashboard deberá mostrar los movimientos recientes del usuario.

## RF-DASHBOARD-013 — Período configurable

El usuario deberá poder seleccionar el período utilizado para los datos del dashboard.

Inicialmente se podrá utilizar:

* Este mes.
* Mes anterior.
* Últimos meses.
* Año.
* Rango personalizado.

## RF-DASHBOARD-014 — Personalización

El usuario podrá configurar qué módulos del dashboard desea visualizar y, cuando sea viable, su orden.

---

# 18. Análisis y visualización

FinTrack deberá utilizar visualizaciones únicamente cuando ayuden a comprender los datos.

## RF-ANALYSIS-001 — Distribución

Los gráficos circulares o de dona podrán utilizarse para representar distribución.

Ejemplo:

```text
¿En qué categorías se está gastando el dinero?
```

## RF-ANALYSIS-002 — Comparaciones

Los gráficos de barras podrán utilizarse para comparar:

* Meses.
* Categorías.
* Ingresos.
* Gastos.
* Presupuestos.

## RF-ANALYSIS-003 — Tendencias

Los gráficos de líneas podrán utilizarse para representar evolución temporal.

## RF-ANALYSIS-004 — Progreso

Las barras de progreso podrán utilizarse para:

* Metas.
* Presupuestos.
* Objetivos financieros.

## RF-ANALYSIS-005 — Períodos comparables

El sistema podrá comparar períodos mostrando:

* Diferencia absoluta.
* Diferencia porcentual.

## RF-ANALYSIS-006 — Resumen inteligente

El sistema podrá generar resúmenes basados únicamente en datos calculados.

No deberá proporcionar recomendaciones financieras personalizadas de manera automática en la primera versión.

---

# 19. Calendario financiero

## RF-CALENDAR-001 — Calendario de obligaciones

El sistema deberá mostrar en un calendario las próximas obligaciones financieras.

Podrán aparecer:

* Cuotas de tarjetas.
* Pagos de préstamos.
* Gastos recurrentes.
* Otros compromisos.

## RF-CALENDAR-002 — Fechas futuras

El usuario deberá poder consultar obligaciones futuras.

## RF-CALENDAR-003 — Detalle

El usuario deberá poder consultar información de una obligación desde el calendario.

---

# 20. Notificaciones

## RF-NOTIFICATION-001 — Tarjetas

El sistema deberá poder notificar sobre próximas fechas de pago de tarjetas.

## RF-NOTIFICATION-002 — Gastos recurrentes

El sistema deberá poder notificar sobre compromisos recurrentes.

## RF-NOTIFICATION-003 — Presupuestos

El sistema deberá poder notificar cuando un presupuesto se encuentre cerca de su límite.

## RF-NOTIFICATION-004 — Metas

El sistema deberá poder enviar recordatorios relacionados con las metas.

## RF-NOTIFICATION-005 — Préstamos

El sistema deberá poder notificar sobre próximos pagos de préstamos.

## RF-NOTIFICATION-006 — Ingresos recurrentes

El sistema podrá notificar sobre ingresos recurrentes configurados.

## RF-NOTIFICATION-007 — Canales

Las notificaciones podrán existir:

* Dentro de la aplicación.
* Como notificaciones del dispositivo.

---

# 21. Reportes

FinTrack deberá permitir generar reportes financieros.

## RF-REPORT-001 — Reporte mensual

El sistema deberá permitir generar un reporte correspondiente a un período mensual.

## RF-REPORT-002 — Reporte anual

El sistema deberá permitir generar reportes anuales.

## RF-REPORT-003 — Reporte de gastos

El sistema deberá permitir consultar información detallada de gastos.

## RF-REPORT-004 — Reporte de ingresos

El sistema deberá permitir consultar información detallada de ingresos.

## RF-REPORT-005 — Reporte por categoría

El sistema deberá permitir analizar movimientos agrupados por categoría.

## RF-REPORT-006 — Reporte de tarjetas

El sistema deberá permitir consultar información relacionada con tarjetas y obligaciones.

## RF-REPORT-007 — Exportación

El sistema deberá permitir exportar información financiera.

Los formatos iniciales contemplados son:

* CSV.
* Excel.
* PDF.

---

# 22. Historial y conservación de información

FinTrack deberá diferenciar entre información operacional actual e información histórica.

Cuando una información financiera sea eliminada o desactivada, deberán evaluarse sus efectos sobre los datos históricos y los reportes previamente generados.

Los reportes históricos podrán conservar una representación de la información correspondiente al momento en que fueron generados.

La arquitectura deberá diseñarse posteriormente para evitar que la eliminación de un elemento actual provoque inconsistencias históricas.

---

# 23. Power BI

Power BI será considerado un objetivo posterior del proyecto.

Los datos de FinTrack deberán diseñarse de forma estructurada y consistente para facilitar posteriormente:

* Análisis financiero.
* Modelado de datos.
* Indicadores.
* Tendencias.
* Comparaciones.
* Dashboards externos.

La primera etapa será generar datos limpios y exportables.

La integración directa con Power BI se definirá posteriormente.

---

# 24. Funcionamiento sin conexión

## RF-OFFLINE-001 — Registro offline

La aplicación deberá permitir registrar determinados movimientos cuando no exista conexión a Internet.

## RF-OFFLINE-002 — Consulta offline

El usuario podrá consultar información previamente sincronizada cuando no tenga conexión.

## RF-OFFLINE-003 — Sincronización

Cuando vuelva la conexión, los datos registrados localmente deberán sincronizarse con el servidor.

## RF-OFFLINE-004 — Control de duplicados

El sistema deberá evitar que una misma operación sea registrada dos veces durante el proceso de sincronización.

## RF-OFFLINE-005 — Manejo de conflictos

La arquitectura deberá contemplar mecanismos para manejar posibles conflictos entre información local y remota.

La estrategia concreta de sincronización se definirá durante el diseño técnico.

---

# 25. Experiencia de usuario

FinTrack deberá tener una interfaz:

* Minimalista.
* Elegante.
* Intuitiva.
* Visual.
* Didáctica.
* Fácil de utilizar.

La información financiera deberá presentarse de manera comprensible incluso para un usuario que no tenga conocimientos financieros avanzados.

## 25.1 Navegación

Se contempla inicialmente una navegación principal similar a:

```text
Inicio
Análisis
Agregar
Cuentas
Perfil
```

Las funciones secundarias podrán accederse desde las secciones correspondientes sin saturar la navegación principal.

## 25.2 Animaciones

La aplicación podrá incluir:

* Transiciones.
* Microinteracciones.
* Animaciones de progreso.
* Animaciones de confirmación.
* Estados visuales.
* Transiciones entre pantallas.

Las animaciones no deberán afectar la claridad ni el rendimiento.

## 25.3 Estados de interfaz

Las pantallas deberán contemplar como mínimo:

* Estado normal.
* Estado vacío.
* Estado de carga.
* Estado de error.
* Estado sin conexión.
* Confirmaciones.
* Operaciones exitosas.

---

# 26. Requisitos no funcionales

## RNF-001 — Multiplataforma

La aplicación deberá poder ejecutarse inicialmente en:

* Android.
* iOS.

## RNF-002 — Seguridad

La información financiera deberá transmitirse y almacenarse utilizando mecanismos adecuados de seguridad.

## RNF-003 — Privacidad

Los datos financieros de un usuario no deberán estar disponibles para otros usuarios.

## RNF-004 — Rendimiento

Las operaciones comunes deberán responder de manera suficientemente rápida para proporcionar una experiencia fluida.

## RNF-005 — Mantenibilidad

El sistema deberá organizarse de forma que permita modificar y ampliar funcionalidades sin afectar innecesariamente otras partes.

## RNF-006 — Escalabilidad

La arquitectura deberá permitir agregar funcionalidades futuras sin necesidad de reconstruir completamente el sistema.

## RNF-007 — Testabilidad

Las partes principales del sistema deberán poder probarse de manera independiente.

## RNF-008 — Documentación

Las decisiones importantes del proyecto deberán documentarse.

## RNF-009 — Consistencia financiera

Los cálculos de saldos, deudas, transferencias y movimientos deberán mantener consistencia entre las diferentes vistas del sistema.

## RNF-010 — Trazabilidad

Las operaciones financieras importantes deberán poder rastrearse mediante su información histórica.

---

# 27. Funcionalidades futuras

Las siguientes funcionalidades se consideran parte de la evolución futura de FinTrack:

### 27.1 Widget de acceso rápido

Posibilidad de registrar rápidamente:

* Gasto.
* Ingreso.
* Transferencia.

Desde la pantalla de inicio del dispositivo.

### 27.2 Cuentas compartidas

Permitir administrar finanzas entre varios usuarios.

### 27.3 Integraciones bancarias

Importar automáticamente movimientos desde instituciones financieras compatibles.

### 27.4 Múltiples monedas

Permitir gestionar diferentes monedas y conversiones.

### 27.5 Inteligencia artificial

Posibles funciones futuras:

* Clasificación automática.
* Resúmenes avanzados.
* Consultas sobre los propios datos.
* Detección de patrones.

Estas funciones deberán evaluarse posteriormente y no forman parte del núcleo inicial.

### 27.6 Power BI avanzado

Integración directa y automatizada con Power BI.

### 27.7 Finanzas avanzadas de tarjetas

Implementación de modelos detallados de:

* Intereses.
* Cargos.
* Comisiones.
* Diferentes condiciones financieras.

---

# 28. Criterios generales del sistema

FinTrack deberá cumplir los siguientes principios funcionales:

1. Una transferencia entre cuentas propias no deberá considerarse ingreso ni gasto.
2. Un retiro de efectivo no deberá considerarse gasto.
3. Gastar posteriormente ese efectivo sí deberá generar un gasto.
4. Recibir un préstamo no deberá considerarse ingreso.
5. Pagar un préstamo no deberá considerarse gasto ordinario.
6. Comprar con tarjeta de crédito deberá generar deuda.
7. Pagar una tarjeta deberá disminuir la deuda y el saldo de la cuenta utilizada.
8. Mover dinero hacia una meta no deberá convertirse automáticamente en un gasto.
9. Retirar dinero de una meta deberá quedar registrado.
10. Los presupuestos deberán informar y alertar, pero no bloquear gastos.
11. Una meta podrá permitir contribuciones variables.
12. Las cuentas desactivadas deberán poder conservar su historial.
13. Las operaciones sensibles deberán contar con protección adicional.
14. Cada usuario deberá tener aislamiento completo de sus datos.
15. La información histórica deberá conservarse de manera coherente.
16. El sistema deberá funcionar parcialmente sin conexión.
17. Los datos deberán mantenerse estructurados para futuros análisis mediante Power BI.

---

# 29. Prioridades del proyecto

Para evitar que el proyecto crezca de manera descontrolada, las funcionalidades se clasificarán durante las siguientes fases.

## Prioridad alta — Núcleo

* Autenticación.
* Usuarios.
* Cuentas.
* Ingresos.
* Gastos.
* Transferencias.
* Efectivo.
* Categorías.
* Dashboard básico.
* Historial.
* Presupuestos.
* Reportes básicos.

## Prioridad media — Expansión

* Tarjetas.
* Cuotas.
* Préstamos.
* Metas.
* Gastos recurrentes.
* Calendario.
* Notificaciones.
* Funcionamiento offline.
* Exportaciones avanzadas.

## Prioridad futura

* Intereses avanzados.
* Integraciones bancarias.
* Power BI directo.
* Widget.
* Cuentas compartidas.
* Múltiples monedas.
* IA avanzada.
* Funcionalidades financieras avanzadas.

---

# 30. Criterio de finalización de requisitos

Esta versión del documento se considerará aprobada cuando:

* Los módulos principales estén identificados.
* Las funcionalidades principales estén descritas.
* No existan contradicciones importantes.
* Las reglas financieras principales estén claramente diferenciadas de los requisitos.
* Las funcionalidades futuras estén separadas del núcleo inicial.
* Los requisitos puedan utilizarse posteriormente para construir los casos de uso.
* El documento pueda servir como referencia para el diseño del dominio, base de datos, API y aplicación móvil.

---

# 31. Próximo documento

Una vez aprobado este documento, el siguiente documento será:

```text
02-reglas-negocio.md
```

En él se definirán las reglas que determinan **cómo debe comportarse FinTrack financieramente**.

Ejemplo:

```text
RF-TRANSACTION-003
El sistema debe permitir transferir dinero entre cuentas.

RN-001
Una transferencia entre cuentas propias no debe contabilizarse
como ingreso ni como gasto.
```

Esta separación permitirá posteriormente pasar de:

```text
REQUISITOS
    ↓
REGLAS DE NEGOCIO
    ↓
CASOS DE USO
    ↓
MODELO DE DOMINIO
    ↓
BASE DE DATOS
    ↓
ARQUITECTURA
    ↓
API
    ↓
APLICACIÓN
```

**Fin del documento.**
