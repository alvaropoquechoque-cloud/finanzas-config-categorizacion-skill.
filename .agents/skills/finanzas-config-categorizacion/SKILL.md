---
name: finanzas-config-categorizacion
description: Administra la configuración, catálogos, categorías y reglas automáticas de categorización del workflow financiero de Sommos. Mantiene la coherencia entre Transacciones, P&L, CxC, CxP, presupuesto y estados financieros sin confundir categorización bancaria con devengo contable.
---

# Finanzas Sommos — Configuración y Categorización

## Propósito

Mantener y auditar la configuración maestra del workflow financiero de Sommos.

Esta skill es responsable de:

- catálogos financieros;
- categorías;
- tipos de movimiento;
- estados;
- países;
- monedas;
- cuentas y medios de pago;
- responsables;
- proyectos/clientes;
- reglas automáticas de categorización;
- consistencia de nombres entre las distintas pestañas del modelo.

Esta skill **no es responsable de registrar transacciones, calcular tipo de cambio, gestionar CxC/CxP ni construir estados financieros**.

Su responsabilidad es garantizar que el resto del sistema trabaje sobre una taxonomía consistente y controlada.

---

# Archivo principal

- Spreadsheet: `Finanzas Sommos — Workflow y Control`
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

El Google Sheet vivo es la fuente de verdad sobre:

- nombres actuales de pestañas;
- encabezados;
- catálogos;
- categorías disponibles;
- reglas activas;
- estructura vigente.

Si una instrucción histórica o documentación de GitHub contradice al Google Sheet vivo, detenerse y revisar antes de modificar.

---

# Pestañas principales

Esta skill opera principalmente sobre:

- `Config`
- `Reglas categorización`

También debe consultar cuando sea necesario:

- `Transacciones`
- `Operative incomes`
- `Real S&A`
- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`
- `Sueldos 2026`
- `Real P&L`
- `Cash Flow`
- `Balance Sheet`
- `Presupuesto`
- `Bancos`
- `Runway Mensual`
- `Dashboard`
- `TC BCB`

No modificar estas pestañas auxiliares desde esta skill salvo que el usuario lo solicite expresamente y el cambio sea estrictamente necesario para validar una modificación de configuración.

---

# Principio fundamental: categorización ≠ devengo

La categorización de `Transacciones` define cómo se clasifica un movimiento bancario u operativo.

**No determina por sí sola cuándo nace un ingreso o un gasto contable.**

El modelo de Sommos distingue:

## Caja / movimientos realizados

`Transacciones`

Representa:

- movimientos bancarios;
- cobros;
- pagos;
- transferencias;
- cash real o movimientos pendientes planificados.

## Devengo de ingresos

`Operative incomes`

Determina principalmente:

- ingreso operativo por periodo;
- montos a facturar;
- forecast comercial;
- base de CxC operativa;
- líneas de ingresos del P&L.

## Devengo de gastos

`Real S&A`

Determina principalmente:

- gasto operativo por periodo;
- obligaciones recurrentes;
- base de CxP;
- líneas de S&A del P&L.

## Sueldos

`Sueldos 2026`

Determina el gasto y planificación de nómina.

`CxP Sueldos` controla:

- devengo;
- pagos;
- adelantos;
- saldo pendiente.

Por lo tanto:

**una regla de categorización nunca debe crear, eliminar o cambiar automáticamente un devengo en `Operative incomes`, `Real S&A` o `Sueldos 2026`.**

---

# Config

`Config` es el catálogo maestro del workflow.

Antes de modificar cualquier valor:

1. leer la estructura viva de la pestaña;
2. identificar qué listas dependen del valor;
3. comprobar si el valor ya existe con otra variante;
4. revisar el impacto en `Reglas categorización`;
5. revisar el impacto potencial en `Transacciones`.

No asumir posiciones de columnas por memoria.

---

# Catálogos

Los catálogos pueden incluir, entre otros:

- País
- Moneda
- Tipo de transacción
- Área
- Categoría
- Estado conciliación
- Sí/No
- Proyecto / cliente
- Estado CxC
- Estado CxP
- Estado presupuesto
- Estado pago
- Cuenta / medio

La estructura exacta debe obtenerse siempre del Sheet vivo.

---

# Regla de nombres

Los valores maestros deben ser:

- únicos;
- consistentes;
- estables;
- reutilizables entre pestañas.

Evitar crear variantes como:

- `BancoSol`
- `Banco Sol`
- `BANCO SOL`

si conceptualmente representan la misma entidad.

Antes de añadir un valor nuevo:

1. buscar coincidencias exactas;
2. buscar variantes ortográficas;
3. buscar abreviaciones;
4. comprobar si existe bajo otro nombre;
5. consultar al usuario si existe ambigüedad real.

---

# Categorías financieras

## Regla principal

**No inventar categorías.**

Toda categoría utilizada en `Transacciones` debe existir en el catálogo vivo de `Config`.

Las categorías deben mantenerse alineadas con la estructura financiera utilizada por Sommos.

Entre las categorías conocidas actualmente pueden aparecer:

### Ingresos operativos

- `Full new integration incomes`
- `Full Integration monthly maintenance fee`
- `Proof of concept incomes`
- `Transactions Fee`
- `Extra features development income`
- `Others`

### Costos y gastos

- `IT salaries`
- `Platform cost`
- `Softwares for development`
- `Sales cost`
- `Fletes`
- `RH expenses`
- `Administrative expenses`
- `Sales expenses`
- `Product expenses`
- `Startup Chile`
- `Bank fees`
- `Travel`
- `Innovatech`
- `Contingency`
- `Operative salaries`
- `Marketing services`
- `Outsourced services`
- `Finance Salary`
- `RH Salary`
- `Sales salaries`
- `Taxes`

### Financiamiento y otros

- `Bank interest earned`
- `Financial expense`
- `Exchange rate differences`
- `Other financing cash flow`
- `Shareholder loan received (non-interest)`
- `Transferencias internas`

Esta lista es referencial.

**El catálogo vivo en `Config` prevalece siempre.**

---

# Categoría y línea contable

No crear una categoría únicamente porque exista una línea similar en el P&L.

Antes de añadir una nueva categoría evaluar:

1. si ya existe una categoría equivalente;
2. si la diferencia es realmente contable;
3. si solo se necesita mayor detalle en la descripción;
4. si puede utilizarse Responsable/Proyecto para diferenciar;
5. si crear la categoría afectaría P&L, presupuesto o reporting.

La taxonomía debe mantenerse suficientemente granular para análisis financiero, pero no fragmentarse innecesariamente.

---

# Reglas de categorización

`Reglas categorización` contiene la lógica que permite clasificar automáticamente las transacciones a partir de texto y otros criterios.

Conceptualmente una regla puede utilizar:

- palabra o frase;
- tipo de transacción;
- categoría destino;
- estado activa/inactiva;
- responsable/proyecto opcional;
- otros filtros definidos en la tabla viva.

La primera regla activa que coincida puede determinar la categoría final.

Por este motivo, **el orden y la especificidad de las reglas importan**.

---

# Prioridad de reglas

Una regla específica debe ir antes que una regla genérica cuando ambas puedan coincidir.

Ejemplo conceptual:

Incorrecto:

1. `GOOGLE` → Administrative expenses
2. `GOOGLE CLOUD` → Platform cost

La primera regla capturaría también Google Cloud.

Correcto:

1. `GOOGLE CLOUD` → Platform cost
2. `GOOGLE` → Administrative expenses

Siempre revisar colisiones antes de agregar una nueva regla.

---

# Coincidencias parciales

Las reglas suelen operar buscando palabras o frases dentro de la descripción de una transacción.

Por lo tanto:

- evitar términos demasiado cortos;
- evitar palabras genéricas;
- evitar nombres que puedan aparecer en muchos proveedores;
- preferir identificadores específicos;
- utilizar Responsable/Proyecto cuando ayude a eliminar ambigüedad.

Ejemplos de términos peligrosamente genéricos:

- `PAGO`
- `TRANSFER`
- `SERVICIO`
- `COMISION`
- `GOOGLE`

No crear una regla genérica sin revisar qué movimientos históricos coincidirían con ella.

---

# Regla crítica: no recategorizar históricos accidentalmente

Antes de activar o modificar una regla:

1. buscar en `Transacciones` todas las descripciones que podrían coincidir;
2. revisar sus categorías actuales;
3. estimar cuántas filas cambiarían;
4. comprobar si pertenecen a distintos conceptos;
5. solamente entonces modificar la regla.

Una regla nueva nunca debe recategorizar meses históricos silenciosamente sin validación.

Si puede afectar movimientos históricos relevantes:

- informar al usuario;
- mostrar ejemplos;
- solicitar confirmación cuando el cambio sea material.

---

# Tipo de movimiento

La categorización debe respetar el `Tipo` de la transacción.

Un mismo texto puede requerir reglas distintas dependiendo de si se trata de:

- Ingreso
- Egreso
- Transferencia

No crear una regla de ingreso que pueda aplicarse a un egreso o viceversa.

Consultar los valores exactos permitidos en `Config`.

---

# Transferencias internas

Las transferencias internas deben clasificarse de forma separada del resultado operativo.

Conceptualmente:

- no son ingresos;
- no son gastos;
- no forman parte de CxC;
- no forman parte de CxP;
- sí afectan cuentas bancarias.

La categoría utilizada por el modelo es:

`Transferencias internas`

No categorizar una transferencia entre cuentas de Sommos como ingreso o gasto solamente porque el extracto de una cuenta muestre entrada o salida.

---

# Grants y financiamiento

Programas conocidos pueden incluir:

- INNOVATECH
- Startup Perú
- INCOFIN
- FIID Guatemala

Los desembolsos de este tipo utilizan normalmente:

`Other financing cash flow`

No clasificarlos automáticamente como ingreso operativo ordinario.

La categorización financiera debe distinguir entre:

- ventas / ingresos operativos;
- grants;
- préstamos;
- aportes;
- financiamiento;
- devoluciones;
- intereses.

La existencia de una categoría no determina por sí sola cómo debe reconocerse el devengo.

---

# Intereses

Distinguir:

## Interés ganado por bancos

`Bank interest earned`

## Interés pagado o devengado

`Financial expense`

## Diferencias cambiarias

`Exchange rate differences`

No mezclar estas categorías con:

- Bank fees;
- Other financing cash flow;
- Administrative expenses.

---

# Bank fees

Comisiones bancarias operativas deben utilizar la categoría configurada para:

`Bank fees`

No clasificar como Bank fees:

- intereses;
- diferencias de cambio;
- transferencias internas;
- impuestos;
- financiamiento.

---

# Outsourced services

Proveedores tercerizados como PPO o Big Picture pueden utilizar:

`Outsourced services`

La clasificación depende del concepto económico, no solamente del nombre del proveedor.

Ejemplo:

una transacción relacionada con un proveedor puede corresponder a otro concepto si el respaldo documental así lo indica.

---

# Innovatech

`Innovatech` es una categoría específica utilizada en el modelo.

No confundir:

- gastos relacionados con Innovatech;
- desembolsos del programa de financiamiento INNOVATECH.

Los gastos pueden categorizarse como:

`Innovatech`

Los desembolsos de financiamiento/grant pueden corresponder a:

`Other financing cash flow`

La descripción y contexto deben determinar cuál aplica.

---

# Responsable / Proyecto

Cuando una regla pueda aplicarse únicamente a un proyecto, cliente o responsable específico, utilizar el filtro correspondiente si existe en `Reglas categorización`.

Esto es preferible a crear categorías duplicadas.

Ejemplo conceptual:

Una misma descripción puede pertenecer a:

- operación general;
- un proyecto específico;
- Innovatech;
- un cliente.

El campo Proyecto/Responsable puede resolver la ambigüedad sin fragmentar la taxonomía.

---

# Qué hacer cuando no existe una regla

Si una transacción no puede clasificarse con seguridad:

usar:

`Por categorizar`

o el valor equivalente definido en el Sheet vivo.

No forzar una categoría solo para eliminar pendientes.

Una transacción pendiente de categorización es preferible a una transacción incorrectamente clasificada.

---

# Creación de nuevas reglas

Antes de crear una regla:

1. leer los encabezados actuales;
2. identificar la descripción real del movimiento;
3. revisar el Tipo;
4. revisar Proyecto/Responsable;
5. buscar reglas existentes similares;
6. buscar movimientos históricos que coincidan;
7. elegir la categoría existente correcta;
8. ubicar la regla en el orden adecuado;
9. activar únicamente cuando la coincidencia sea suficientemente segura.

---

# Modificación de reglas

Antes de modificar una regla existente:

1. identificar por qué está fallando;
2. revisar cuántas transacciones utiliza;
3. comprobar si el problema es:
   - texto demasiado genérico;
   - categoría incorrecta;
   - Tipo incorrecto;
   - Responsable incorrecto;
   - prioridad incorrecta;
4. corregir el mínimo necesario.

No reemplazar reglas ampliamente utilizadas sin revisar su impacto histórico.

---

# Eliminación de reglas

Preferir desactivar antes que eliminar cuando exista valor histórico o de auditoría.

Eliminar una regla únicamente cuando:

- sea duplicada;
- sea claramente incorrecta;
- nunca deba volver a utilizarse;
- el usuario haya solicitado limpieza definitiva.

---

# Validaciones antes de escribir

Antes de cambiar `Config` o `Reglas categorización`:

1. leer el rango relevante en vivo;
2. confirmar encabezados;
3. buscar duplicados;
4. revisar las reglas relacionadas;
5. revisar ejemplos reales en `Transacciones`;
6. comprobar si el valor es usado por otras pestañas;
7. evaluar el impacto en históricos;
8. evitar cambiar simultáneamente múltiples reglas no relacionadas.

---

# Validaciones después de escribir

Después de modificar configuración o reglas:

1. releer exactamente las celdas modificadas;
2. verificar que la regla quede activa/inactiva según lo esperado;
3. revisar las transacciones que deberían coincidir;
4. revisar varias transacciones que NO deberían coincidir;
5. comprobar que no aparezcan nuevas filas `Por categorizar` inesperadas;
6. comprobar que no se hayan recategorizado movimientos históricos incorrectamente;
7. buscar errores como:
   - `#REF!`
   - `#VALUE!`
   - `#N/A`
   - `#ERROR!`

Si el cambio afecta categorías utilizadas en estados financieros, revisar adicionalmente:

- `Real P&L`
- `Cash Flow`
- `Balance Sheet`
- `Dashboard`

No reportar el cambio como terminado hasta releer el resultado en el Sheet vivo.

---

# Regla de validación histórica

Los meses ya conciliados no deben cambiar como consecuencia accidental de una nueva regla.

Actualmente agosto de 2026 es un mes cerrado y validado dentro del workflow.

Si una modificación cambia categorías históricas de un mes cerrado:

- detenerse;
- identificar las filas afectadas;
- explicar el impacto;
- no asumir que la nueva categorización es correcta solamente porque la regla sea más reciente.

---

# No usar categorización para cuadrar estados

Nunca crear o cambiar una categoría con el único objetivo de:

- hacer cuadrar el P&L;
- hacer cuadrar el Cash Flow;
- hacer cuadrar el Balance Sheet;
- reducir una diferencia bancaria;
- eliminar un check.

Primero identificar la causa económica y documental.

La categorización debe representar la naturaleza real del movimiento.

---

# No inventar datos

Esta skill nunca debe inventar:

- categorías;
- proyectos;
- responsables;
- países;
- monedas;
- bancos;
- cuentas;
- estados;
- tipos de movimiento.

Si falta información:

- mantener el estado pendiente correspondiente;
- preguntar al usuario cuando la ambigüedad sea material.

---

# Relación con el modelo financiero

La taxonomía configurada aquí alimenta indirectamente:

`Transacciones`
→ análisis de movimientos
→ conciliación
→ reporting
→ Dashboard

Pero el modelo de devengo sigue su propia lógica:

`Operative incomes`
→ CxC
→ P&L

`Real S&A`
→ CxP
→ P&L

`Sueldos 2026`
→ CxP Sueldos
→ P&L

Y posteriormente:

`P&L`
→ `Balance Sheet`
→ `Cash Flow`
→ `Runway Mensual`
→ `Dashboard`

No romper esta separación conceptual.

---

# Reglas de seguridad financiera

- No inventar categorías.
- No recategorizar históricos sin revisar impacto.
- No crear reglas demasiado genéricas.
- No utilizar categorización para cuadrar estados.
- No confundir caja con devengo.
- No confundir grants con ingresos operativos.
- No confundir financiamiento con ventas.
- No confundir transferencias internas con ingresos o gastos.
- No eliminar reglas históricas sin razón.
- Leer antes de escribir.
- Releer después de escribir.
- El Google Sheet vivo prevalece sobre documentación histórica.
- Nunca reportar un cambio como completado sin verificar el resultado real.

---

# Coordinación con otras skills

## `finanzas-transacciones-tc`

Usar para:

- importar extractos;
- crear o actualizar movimientos;
- tipo de cambio;
- monto USD;
- transferencias;
- conciliación a nivel transacción.

## `finanzas-cxc-cxp`

Usar para:

- cuentas por cobrar;
- cuentas por pagar;
- grants pendientes;
- vencimientos;
- pagos/cobros;
- CxP Sueldos;
- roll-forward de saldos.

## `finanzas-presupuesto-bancos`

Usar para:

- Presupuesto;
- Bancos;
- saldos bancarios;
- conciliación de cierre;
- Budget vs P&L.

## `finanzas-runway-dashboard`

Usar para:

- runway;
- escenarios de caja;
- KPIs;
- Dashboard;
- alertas ejecutivas.

## `finanzas-estados-financieros`

Cuando exista, usar para:

- Real P&L;
- Cash Flow;
- Balance Sheet;
- checks del modelo de tres estados.

## `finanzas-cierre-mensual`

Cuando exista, usar para:

- orquestar el cierre mensual completo;
- comprobar bancos cerrados;
- transacciones por categorizar;
- movimientos sin conciliar;
- CxC/CxP;
- P&L;
- Cash Flow;
- Balance Sheet;
- Dashboard;
- estado final `✓ CERRADO`.

---

# Alcance de esta skill

Esta skill debe concentrarse en:

- configuración maestra;
- taxonomía;
- categorías;
- reglas;
- prioridades;
- consistencia de nombres;
- validaciones de categorización.

No debe convertirse en una skill general de finanzas.

Su objetivo es que **todos los demás componentes del workflow utilicen un lenguaje financiero común, estable y auditable**.
