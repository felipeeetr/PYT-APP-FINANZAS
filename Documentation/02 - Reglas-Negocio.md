# FinTrack — Reglas de Negocio

**Versión:** 1.0
**Estado:** Borrador para revisión
**Proyecto:** FinTrack
**Documento:** Reglas de negocio

---

# 1. Propósito

Este documento define las reglas que determinan cómo debe comportarse FinTrack desde el punto de vista financiero y funcional.

Mientras el documento de requisitos define **qué debe hacer el sistema**, este documento establece **bajo qué condiciones y reglas debe hacerlo**.

Las reglas aquí definidas deberán ser consideradas posteriormente durante:

* Diseño del dominio.
* Casos de uso.
* Diseño de base de datos.
* Diseño de API.
* Implementación del backend.
* Implementación de la aplicación móvil.
* Pruebas.

---

# 2. Principios generales

## RN-001 — Aislamiento de usuarios

Cada usuario deberá tener acceso únicamente a su propia información financiera.

Un usuario no podrá consultar, modificar o eliminar información perteneciente a otro usuario.

---

## RN-002 — Moneda inicial

Todas las operaciones financieras de la primera versión utilizarán pesos colombianos (COP).

El soporte para múltiples monedas queda fuera del alcance inicial.

---

## RN-003 — Valores monetarios positivos

Los valores monetarios registrados para operaciones financieras deberán ser mayores que cero.

La dirección del movimiento se determinará mediante el tipo de operación y no mediante valores negativos introducidos manualmente por el usuario.

---

## RN-004 — Consistencia de saldos

Toda operación que afecte el saldo de una cuenta deberá mantener consistencia entre:

* Movimiento registrado.
* Saldo de origen.
* Saldo de destino, cuando corresponda.
* Historial.

---

## RN-005 — No duplicación financiera

Una misma operación financiera no deberá afectar dos veces los saldos, estadísticas o deudas como consecuencia de un error de registro o sincronización.

---

# 3. Reglas de cuentas

## RN-006 — Propiedad de las cuentas

Toda cuenta financiera deberá pertenecer a un único usuario.

---

## RN-007 — Saldo de cuentas normales

Las cuentas financieras normales no deberán permitir saldos negativos como resultado de operaciones ordinarias.

La aplicación deberá validar la disponibilidad antes de realizar una operación que disminuya el saldo.

---

## RN-008 — Desactivación de cuentas

Desactivar una cuenta no deberá eliminar automáticamente su historial financiero.

La cuenta podrá dejar de estar disponible para nuevas operaciones, pero su información histórica deberá conservarse.

---

## RN-009 — Eliminación permanente de cuenta

La eliminación permanente de una cuenta será una operación sensible.

Antes de ejecutarla, el sistema deberá:

1. Informar al usuario sobre sus consecuencias.
2. Solicitar confirmación.
3. Requerir una autenticación adicional cuando corresponda.

---

## RN-010 — Cuenta con historial

Cuando una cuenta posea movimientos históricos, el sistema deberá priorizar su desactivación sobre la eliminación automática de la información histórica.

---

# 4. Reglas de movimientos

## RN-011 — Tipos principales de movimiento

FinTrack reconocerá inicialmente tres tipos principales:

* Ingreso.
* Gasto.
* Transferencia.

---

## RN-012 — Ingreso

Un ingreso representa dinero recibido por el usuario que incrementa los recursos disponibles.

Los ingresos deberán afectar positivamente la cuenta correspondiente.

---

## RN-013 — Gasto

Un gasto representa dinero utilizado para adquirir bienes, servicios u otros conceptos de consumo.

Un gasto deberá disminuir el recurso financiero utilizado.

---

## RN-014 — Transferencia

Una transferencia representa el movimiento de dinero entre cuentas pertenecientes al mismo usuario.

Una transferencia no representa un ingreso ni un gasto.

---

## RN-015 — Transferencia entre cuentas propias

Una transferencia deberá:

1. Disminuir el saldo de la cuenta origen.
2. Aumentar el saldo de la cuenta destino.
3. Mantener el mismo valor financiero en ambas operaciones.
4. No incrementar los ingresos.
5. No incrementar los gastos.

Ejemplo:

```text
Bancolombia → Nequi
$300.000
```

Resultado:

```text
Bancolombia: -$300.000
Nequi:       +$300.000
```

---

## RN-016 — Cuenta origen y destino

Una transferencia deberá identificar una cuenta origen y una cuenta destino.

Ambas deberán pertenecer al mismo usuario.

---

## RN-017 — Transferencia a la misma cuenta

Una cuenta no deberá poder transferirse dinero hacia sí misma.

---

## RN-018 — Saldo suficiente

Una operación que disminuya una cuenta normal no deberá poder ejecutarse si el saldo disponible resulta insuficiente.

---

# 5. Reglas de efectivo

## RN-019 — Efectivo como cuenta

El efectivo podrá representarse como una cuenta financiera administrada por el usuario.

---

## RN-020 — Retiro de efectivo

Retirar dinero de una cuenta bancaria para convertirlo en efectivo no constituye un gasto.

Ejemplo:

```text
Bancolombia: -$300.000
Efectivo:    +$300.000
```

La operación representa únicamente una transferencia de recursos.

---

## RN-021 — Gasto posterior con efectivo

Cuando el usuario utilice posteriormente el efectivo para realizar una compra, esa operación sí deberá registrarse como gasto.

Ejemplo:

```text
Efectivo: -$50.000
Gasto:     $50.000
```

---

# 6. Reglas de eliminación y anulación

## RN-022 — Eliminación de movimiento

Eliminar un movimiento deberá ser una operación controlada.

El sistema deberá evaluar las consecuencias de la eliminación sobre:

* Saldos.
* Estadísticas.
* Presupuestos.
* Reportes.
* Historial.

---

## RN-023 — Anulación de movimiento

Anular un movimiento no deberá eliminar completamente su registro histórico.

El movimiento deberá conservarse con un estado que permita identificarlo como:

**ANULADO**

---

## RN-024 — Efecto financiero de una anulación

Un movimiento anulado no deberá continuar afectando:

* Saldos operativos.
* Estadísticas.
* Presupuestos.
* Cálculos financieros activos.

Sin embargo, deberá conservarse la información necesaria para mantener trazabilidad.

---

# 7. Reglas de corrección y reembolsos

## RN-025 — Corrección de gastos

Cuando un gasto haya sido registrado incorrectamente, el usuario podrá modificarlo.

La modificación deberá actualizar los cálculos correspondientes.

---

## RN-026 — Reembolso

Inicialmente, un reembolso se gestionará mediante la edición o corrección del gasto correspondiente.

La posibilidad de implementar posteriormente un historial detallado de modificaciones queda abierta.

---

# 8. Reglas de tarjetas de crédito

Las tarjetas de crédito deberán tratarse como entidades diferentes de las cuentas financieras normales.

---

## RN-027 — Tarjeta como obligación financiera

Una tarjeta de crédito representa una obligación financiera y no deberá comportarse como una cuenta bancaria normal.

---

## RN-028 — Compra con tarjeta

Una compra realizada con tarjeta deberá incrementar la deuda de la tarjeta.

No deberá disminuir inmediatamente el saldo de una cuenta bancaria.

---

## RN-029 — Crédito disponible

El crédito disponible deberá corresponder al límite de crédito menos la deuda correspondiente, teniendo en cuenta las operaciones válidas registradas.

---

## RN-030 — Compra a cuotas

Cuando una compra se registre a cuotas, deberá conservarse la relación entre:

* Compra original.
* Número de cuotas.
* Valor de las cuotas.
* Fechas correspondientes.
* Estado de cada cuota.

---

## RN-031 — Cuotas futuras

Las cuotas pendientes deberán poder identificarse como obligaciones futuras.

---

## RN-032 — Pago de tarjeta

Cuando el usuario pague una tarjeta:

1. Deberá disminuir el saldo de la cuenta utilizada.
2. Deberá disminuir la deuda de la tarjeta.
3. No deberá registrarse como un gasto ordinario.

---

## RN-033 — Pago parcial

Los pagos parciales deberán disminuir parcialmente la deuda.

El sistema deberá mostrar claramente el saldo restante.

---

## RN-034 — Fechas de tarjeta

Las fechas de corte y pago configuradas para la tarjeta deberán utilizarse para organizar las obligaciones futuras.

El usuario podrá modificar estas fechas cuando sea necesario.

---

## RN-035 — Intereses y cargos

Las reglas avanzadas relacionadas con intereses, comisiones y cargos financieros no forman parte de la primera definición funcional.

Se implementarán posteriormente cuando se hayan establecido las reglas financieras correspondientes.

---

# 9. Reglas de préstamos

## RN-036 — Préstamo recibido

Recibir dinero mediante un préstamo deberá:

* Incrementar el dinero disponible.
* Incrementar la deuda del usuario.

No deberá contabilizarse como ingreso.

---

## RN-037 — Préstamo otorgado

Cuando el usuario preste dinero a otra persona:

* Deberá disminuir el dinero disponible correspondiente.
* Deberá registrarse el valor que el tercero debe devolver.

---

## RN-038 — Pago de préstamo

El pago de una deuda deberá:

* Disminuir el saldo de la cuenta utilizada.
* Disminuir la deuda correspondiente.

No deberá contabilizarse como un gasto ordinario.

---

## RN-039 — Cobro de préstamo otorgado

Cuando una persona devuelva dinero prestado por el usuario, el sistema deberá registrar el incremento correspondiente de dinero y la disminución de la deuda del tercero.

La devolución del capital no deberá considerarse un ingreso ordinario.

---

## RN-040 — Cuotas de préstamo

Cuando un préstamo tenga cuotas, cada cuota deberá mantener información sobre:

* Valor.
* Fecha.
* Estado.
* Deuda restante.

---

# 10. Reglas de categorías

## RN-041 — Categoría de gasto

Los gastos deberán poder asociarse con una categoría.

---

## RN-042 — Categorías personalizadas

El usuario podrá modificar o crear categorías de acuerdo con sus necesidades.

---

## RN-043 — Historial de categorías

La eliminación o desactivación de una categoría no deberá provocar automáticamente la pérdida de los movimientos históricos asociados.

---

## RN-044 — Sin subcategorías iniciales

La primera versión no utilizará subcategorías.

---

# 11. Reglas de presupuestos

## RN-045 — Presupuesto asociado a categoría

Cada presupuesto deberá estar asociado a una categoría.

---

## RN-046 — Período del presupuesto

Un presupuesto deberá estar asociado a un período determinado.

---

## RN-047 — Cálculo de progreso

El progreso de un presupuesto deberá calcularse utilizando los gastos válidos asociados con la categoría y período correspondiente.

---

## RN-048 — Presupuesto excedido

Superar el límite de un presupuesto no deberá impedir al usuario realizar nuevos gastos.

El sistema deberá informar visualmente que el límite fue superado.

---

## RN-049 — Gastos anulados

Los movimientos anulados no deberán contabilizarse como gastos válidos para el progreso de un presupuesto.

---

# 12. Reglas de compromisos recurrentes

## RN-050 — Compromiso recurrente

Un compromiso recurrente representa una obligación que se repite periódicamente.

---

## RN-051 — Valor habitual

Cada compromiso podrá tener un valor habitual utilizado como referencia para futuras ocurrencias.

---

## RN-052 — Cambio temporal

Si el valor de una ocurrencia cambia, el sistema deberá permitir que el usuario indique que el cambio aplica únicamente a esa ocurrencia.

---

## RN-053 — Cambio permanente

El usuario podrá indicar que un nuevo valor deberá utilizarse para futuras ocurrencias.

---

## RN-054 — Confirmación

El sistema podrá preparar una nueva ocurrencia de un compromiso recurrente para que el usuario la confirme o modifique.

---

# 13. Reglas de metas

## RN-055 — Meta financiera

Una meta representa un objetivo de acumulación de dinero.

---

## RN-056 — Aportes flexibles

El usuario podrá realizar aportes:

* Mayores al recomendado.
* Menores al recomendado.
* Iguales al recomendado.
* Sin realizar aportes durante un período.

El sistema no deberá obligar al usuario a cumplir un aporte específico.

---

## RN-057 — Aporte recomendado

Si la meta posee una fecha objetivo, el sistema podrá calcular un valor de aporte recomendado.

Este valor será informativo.

---

## RN-058 — Meta y gasto

Mover dinero hacia una meta no deberá considerarse automáticamente un gasto.

---

## RN-059 — Retiro de meta

Retirar dinero de una meta deberá quedar registrado como una salida de dinero de la meta.

---

## RN-060 — Procedencia de aportes

El sistema deberá mantener información sobre el origen de los aportes realizados a una meta cuando sea necesario para la trazabilidad.

---

# 14. Reglas del dashboard

## RN-061 — Información calculada

Los valores mostrados en el dashboard deberán calcularse utilizando información financiera válida y consistente.

---

## RN-062 — Movimientos anulados

Los movimientos anulados no deberán afectar los indicadores financieros activos del dashboard.

---

## RN-063 — Transferencias

Las transferencias internas no deberán inflar artificialmente los indicadores de ingresos o gastos.

---

## RN-064 — Períodos

Los indicadores deberán respetar el período seleccionado por el usuario.

---

## RN-065 — Comparaciones

Las comparaciones entre períodos deberán utilizar períodos comparables.

Cuando se muestre una diferencia porcentual, el sistema deberá manejar correctamente los casos en los que el valor de referencia sea cero.

---

# 15. Reglas de reportes

## RN-066 — Datos válidos

Los reportes deberán utilizar información financiera válida de acuerdo con las reglas del sistema.

---

## RN-067 — Transferencias

Las transferencias internas deberán poder identificarse como tales para evitar que se contabilicen incorrectamente como ingresos o gastos.

---

## RN-068 — Anulaciones

Los reportes operativos no deberán considerar movimientos anulados como movimientos financieros activos.

Los reportes históricos podrán conservar información sobre operaciones posteriormente anuladas cuando corresponda.

---

## RN-069 — Exportaciones

Los datos exportados deberán mantener una estructura consistente.

Los formatos iniciales serán:

* CSV.
* Excel.
* PDF.

---

# 16. Reglas del calendario

## RN-070 — Obligaciones futuras

El calendario deberá mostrar únicamente obligaciones y eventos financieros relevantes para el usuario.

---

## RN-071 — Tarjetas

Las cuotas pendientes y fechas de pago deberán poder aparecer en el calendario.

---

## RN-072 — Préstamos

Las cuotas y vencimientos de préstamos deberán poder aparecer en el calendario.

---

## RN-073 — Recurrentes

Los compromisos recurrentes próximos deberán poder aparecer en el calendario.

---

# 17. Reglas de notificaciones

## RN-074 — Configuración

Las notificaciones deberán poder configurarse progresivamente de acuerdo con las preferencias del usuario.

---

## RN-075 — Próximos vencimientos

Las notificaciones podrán generarse antes de fechas importantes relacionadas con:

* Tarjetas.
* Préstamos.
* Compromisos recurrentes.
* Metas.
* Otros eventos configurados.

---

## RN-076 — Presupuestos

Cuando un presupuesto se aproxime al límite configurado, el sistema podrá generar una notificación.

---

# 18. Reglas de seguridad

## RN-077 — Operaciones sensibles

Las operaciones sensibles deberán requerir una confirmación adicional de identidad.

---

## RN-078 — Credenciales

Las contraseñas no deberán almacenarse en texto plano.

---

## RN-079 — Sesiones

Los mecanismos de sesión deberán impedir que un usuario autenticado acceda a información de otro usuario.

---

## RN-080 — Tokens

Los tokens de autenticación deberán manejarse de manera segura tanto en el backend como en el dispositivo.

---

# 19. Reglas de funcionamiento offline

## RN-081 — Registro sin conexión

El usuario podrá registrar determinadas operaciones sin conexión a Internet.

---

## RN-082 — Estado pendiente

Las operaciones creadas sin conexión deberán poder identificarse como pendientes de sincronización.

---

## RN-083 — Sincronización

Cuando vuelva la conexión, las operaciones pendientes deberán enviarse al servidor.

---

## RN-084 — No duplicación durante sincronización

Una operación sincronizada correctamente no deberá volver a registrarse como una nueva operación.

---

## RN-085 — Conflictos

Cuando exista una diferencia entre información local y remota, el sistema deberá aplicar una estrategia definida durante el diseño técnico.

---

# 20. Reglas de historial

## RN-086 — Conservación histórica

Las operaciones financieras importantes deberán conservar la información necesaria para mantener trazabilidad.

---

## RN-087 — Desactivación

Desactivar una cuenta, categoría u otro elemento no deberá provocar automáticamente la eliminación de los movimientos históricos asociados.

---

## RN-088 — Reportes históricos

Los reportes previamente generados podrán conservar una representación histórica de la información correspondiente al momento de generación.

---

# 21. Reglas de estadísticas

## RN-089 — Ingresos

Las estadísticas de ingresos deberán considerar únicamente ingresos válidos.

---

## RN-090 — Gastos

Las estadísticas de gastos deberán considerar únicamente gastos válidos.

---

## RN-091 — Transferencias internas

Las transferencias entre cuentas propias no deberán aumentar artificialmente ingresos o gastos.

---

## RN-092 — Operaciones anuladas

Las operaciones anuladas no deberán afectar las estadísticas financieras activas.

---

# 22. Reglas de patrimonio

## RN-093 — Patrimonio neto

El patrimonio neto deberá calcularse considerando los activos financieros y las obligaciones financieras relevantes registradas en el sistema.

---

## RN-094 — Deudas

Las obligaciones como tarjetas y préstamos deberán considerarse en los cálculos correspondientes de deuda y patrimonio.

---

# 23. Reglas de futuras funcionalidades

## RN-095 — Funcionalidades fuera del núcleo

Las funcionalidades futuras no deberán alterar las reglas fundamentales del núcleo financiero sin una revisión formal de los requisitos y reglas existentes.

---

## RN-096 — Nuevas monedas

La incorporación de múltiples monedas deberá realizarse mediante nuevas reglas específicas y no modificando de manera ambigua las reglas actuales de COP.

---

## RN-097 — Cuentas compartidas

La incorporación de cuentas compartidas deberá incluir nuevas reglas de autorización, propiedad y acceso antes de implementarse.

---

# 24. Prioridad de las reglas

Las reglas financieras fundamentales tendrán prioridad sobre las reglas visuales o de presentación.

En caso de conflicto:

```text
Reglas financieras
        ↓
Reglas de seguridad
        ↓
Reglas de consistencia
        ↓
Presentación de información
```

---

# 25. Principios financieros fundamentales de FinTrack

Las siguientes reglas resumen el comportamiento financiero central de la aplicación:

| Operación                   | Dinero                | Deuda | ¿Ingreso? | ¿Gasto? |
| --------------------------- | --------------------- | ----- | --------- | ------- |
| Registrar ingreso           | ↑                     | —     | Sí        | No      |
| Registrar gasto             | ↓                     | —     | No        | Sí      |
| Transferencia propia        | origen ↓ / destino ↑  | —     | No        | No      |
| Retiro de efectivo          | cuenta ↓ / efectivo ↑ | —     | No        | No      |
| Gasto con efectivo          | ↓                     | —     | No        | Sí      |
| Compra con tarjeta          | —                     | ↑     | No        | Sí*     |
| Pago de tarjeta             | cuenta ↓              | ↓     | No        | No      |
| Recibir préstamo            | ↑                     | ↑     | No        | No      |
| Pagar préstamo              | ↓                     | ↓     | No        | No      |
| Prestar dinero              | ↓                     | —     | No        | No      |
| Recuperar préstamo otorgado | ↑                     | ↓     | No        | No      |
| Aporte a meta               | según origen          | —     | No        | No      |
| Retiro de meta              | según destino         | —     | No        | No      |

* **Nota:** una compra con tarjeta se considera gasto para las estadísticas de consumo, pero no disminuye inmediatamente el saldo de una cuenta bancaria. El tratamiento exacto de su reconocimiento financiero deberá mantenerse consistente con el modelo de tarjetas y cuotas definido durante la implementación.

---

# 26. Relación con los siguientes documentos

Estas reglas servirán como base para los siguientes documentos:

```text
01-requisitos.md
       ↓
02-reglas-negocio.md
       ↓
03-casos-uso.md
       ↓
04-modelo-dominio.md
       ↓
05-base-datos.md
       ↓
06-arquitectura.md
       ↓
07-api.md
       ↓
08-ui-ux.md
       ↓
09-decisiones-tecnicas.md
```

Los casos de uso deberán respetar estas reglas.

El modelo de dominio deberá representar las entidades y comportamientos necesarios para cumplirlas.

La base de datos deberá permitir almacenar la información necesaria para aplicarlas.

El backend deberá implementarlas de forma consistente.

La aplicación móvil deberá reflejarlas correctamente en la interfaz.

---

# 27. Estado del documento

Este documento representa la primera versión formal de las reglas de negocio de FinTrack.

Las reglas podrán modificarse durante el proyecto cuando aparezcan nuevos requisitos, pero cualquier cambio importante deberá quedar documentado y versionado.

**Siguiente documento: `03-casos-uso.md`**
