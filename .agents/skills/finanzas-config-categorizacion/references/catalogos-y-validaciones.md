# Finanzas Sommos — Catálogos y validaciones

## Propósito

Este documento complementa la skill:

`finanzas-config-categorizacion`

Su objetivo es documentar:

- los catálogos maestros utilizados por el workflow financiero;
- las reglas de consistencia entre catálogos;
- las validaciones mínimas antes y después de modificarlos;
- los controles necesarios para evitar romper históricos o estados financieros.

La estructura viva del Google Sheet siempre prevalece sobre este documento.

---

# Archivo principal

- Spreadsheet: `Finanzas Sommos — Workflow y Control`
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`

Pestañas relevantes:

- `Config`
- `Reglas categorización`
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

---

# Principio de fuente de verdad

`Config` contiene los valores maestros que deben reutilizarse en el workflow.

Nunca asumir que este archivo de referencia contiene la lista completa o más reciente.

Antes de agregar o modificar un valor:

1. leer `Config` en vivo;
2. buscar el valor exacto;
3. buscar variantes ortográficas;
4. revisar dónde se utiliza;
5. evaluar el impacto antes de escribir.

---

# Catálogos principales

La pestaña `Config` puede contener catálogos como:

- País
- Moneda
- Tipo de transacción
- Área
- Categoría
- Estado conciliación
- Sí / No
- Proyecto / cliente
- Estado CxC
- Estado CxP
- Estado presupuesto
- Estado pago
- Cuenta / medio

La posición de estos catálogos puede cambiar.

No utilizar números de columna hardcodeados sin leer primero la estructura actual.

---

# País

Los países deben utilizar un nombre canónico único.

Ejemplos de países utilizados por Sommos pueden incluir:

- Bolivia
- Perú
- Chile
- Guatemala
- Estados Unidos

Evitar variantes para el mismo país.

Ejemplo incorrecto:

- USA
- EEUU
- Estados Unidos

como tres valores maestros diferentes si representan el mismo concepto.

Si el Sheet vivo utiliza una forma determinada, respetarla.

---

# Moneda

Monedas conocidas en el workflow:

- USD
- BOB
- SOL / PEN, según la convención viva del Sheet

No crear una nueva variante de moneda sin revisar primero `Config`.

La definición de moneda pertenece a esta skill.

La conversión y tipo de cambio pertenece principalmente a:

`finanzas-transacciones-tc`

---

# Tipo de transacción

Los tipos deben distinguir la naturaleza del movimiento.

Conceptualmente pueden incluir:

- Ingreso
- Egreso
- Transferencia interna

Usar siempre el valor exacto definido en `Config`.

No clasificar transferencias entre cuentas propias como Ingreso o Egreso operativo.

---

# Categorías

## Regla principal

No inventar categorías.

Toda categoría utilizada en:

`Transacciones`

debe existir en `Config`.

La categoría debe representar la naturaleza económica del movimiento.

No crear categorías para:

- nombres individuales de proveedores si ya existe una categoría económica;
- diferencias puramente descriptivas;
- proyectos que pueden identificarse con otro campo;
- cuadrar estados financieros.

---

# Categorías conocidas — ingresos

Entre las categorías utilizadas por el modelo pueden encontrarse:

- `Full new integration incomes`
- `Full Integration monthly maintenance fee`
- `Proof of concept incomes`
- `Transactions Fee`
- `Extra features development income`
- `Others`

Estas categorías se relacionan conceptualmente con las líneas de ingreso de `Real P&L`.

La existencia de una categoría en `Transacciones` no determina por sí sola el devengo del ingreso.

El devengo operativo se controla principalmente desde:

`Operative incomes`

---

# Categorías conocidas — costos y gastos

Entre las categorías utilizadas por el modelo pueden encontrarse:

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

El catálogo vivo prevalece sobre esta lista.

---

# Categorías conocidas — financiamiento y otros

Pueden incluir:

- `Bank interest earned`
- `Financial expense`
- `Exchange rate differences`
- `Other financing cash flow`
- `Shareholder loan received (non-interest)`
- `Transferencias internas`

Mantener claramente separados:

- ingreso operativo;
- grant;
- préstamo;
- aporte;
- interés;
- diferencia cambiaria;
- transferencia interna.

---

# Área

El campo Área debe utilizarse para identificar el área económica o funcional correspondiente.

No crear nuevas áreas únicamente para diferenciar proveedores.

Ejemplo:

un proveedor puede cambiar, pero seguir perteneciendo al mismo concepto o área.

Antes de agregar un Área:

- revisar si ya existe;
- revisar si es realmente una nueva unidad funcional;
- evitar duplicar diferencias de mayúsculas/minúsculas.

---

# Proyecto / cliente

Usar Proyecto / Cliente para aportar detalle sin fragmentar innecesariamente las categorías.

Un proyecto puede permitir distinguir movimientos que utilizan la misma categoría económica.

Ejemplo conceptual:

`Travel`

puede pertenecer a:

- operación general;
- Innovatech;
- un proyecto de cliente.

No crear tres categorías de Travel si Proyecto puede resolver correctamente la separación.

---

# Estado de pago

Los estados deben permitir diferenciar como mínimo:

- obligaciones o cobros pendientes;
- movimientos ya pagados/cobrados.

Un valor conocido utilizado en el workflow es:

`Pagado/Cobrado`

Los valores exactos deben verificarse siempre en `Config`.

No confundir Estado de pago con Estado de conciliación.

---

# Estado de conciliación

La conciliación responde a:

> ¿este movimiento fue contrastado contra la evidencia bancaria correspondiente?

Un valor conocido es:

`Conciliado`

No significa lo mismo que:

`Pagado/Cobrado`

Un movimiento puede estar pagado pero aún necesitar revisión de conciliación.

---

# Valor "Por categorizar"

Cuando la clasificación económica no sea suficientemente segura:

usar el valor vivo equivalente a:

`Por categorizar`

No elegir una categoría arbitraria para dejar el contador en cero.

La prioridad es exactitud, no apariencia de completitud.

---

# Separación entre categorización y devengo

Esta es una regla crítica del modelo actual.

## Transacciones

Representa principalmente:

- cash;
- movimientos bancarios;
- cobros;
- pagos;
- transferencias.

## Operative incomes

Representa principalmente:

- devengo de ingresos;
- monto a facturar;
- forecast comercial.

## Real S&A

Representa principalmente:

- devengo de gastos;
- obligaciones recurrentes;
- forecast de gastos.

## Sueldos 2026

Representa:

- gasto y planificación de nómina.

Por lo tanto:

una categoría en `Transacciones` no debe crear automáticamente un devengo.

---

# Validación antes de crear un valor maestro

Antes de agregar cualquier valor a `Config`:

1. leer la tabla viva;
2. buscar coincidencia exacta;
3. buscar variantes;
4. revisar reglas de categorización;
5. revisar transacciones existentes;
6. determinar si puede utilizarse otro campo existente;
7. comprobar si afecta P&L o reporting;
8. escribir solamente si existe una necesidad real.

---

# Validación después de crear un valor maestro

Después de escribir:

1. releer la celda;
2. confirmar que el valor aparece correctamente;
3. revisar validaciones/listas desplegables relacionadas;
4. comprobar que ninguna fórmula se rompió;
5. comprobar que las reglas existentes sigan siendo válidas;
6. buscar errores:
   - `#REF!`
   - `#VALUE!`
   - `#N/A`
   - `#ERROR!`

No reportar el cambio como completado sin releer el Sheet vivo.

---

# Validación antes de renombrar un valor

Renombrar es más riesgoso que crear.

Antes de renombrar:

1. buscar todas las ocurrencias en `Transacciones`;
2. revisar `Reglas categorización`;
3. revisar `Operative incomes`;
4. revisar `Real S&A`;
5. revisar `Presupuesto`;
6. revisar estados financieros si utilizan texto como criterio;
7. identificar fórmulas con `SUMIF`, `SUMIFS`, `FILTER`, `REGEXMATCH`, `SEARCH` o comparaciones directas.

No renombrar globalmente sin saber qué referencias dependen del texto.

---

# Validación después de renombrar

Comprobar:

- que no quede la variante antigua en movimientos activos;
- que las reglas apunten al nuevo valor;
- que el P&L mantenga sus importes;
- que CxC/CxP mantengan sus saldos;
- que Dashboard no pierda KPIs;
- que no aumenten movimientos `Por categorizar`.

Si cambia un resultado financiero inesperadamente:

detenerse y revisar.

---

# Meses cerrados

Los meses cerrados tienen protección conceptual especial.

Actualmente el workflow reconoce agosto de 2026 como un periodo cerrado y validado.

Un cambio en Config o reglas no debe alterar silenciosamente un periodo cerrado.

Si una nueva configuración afecta un mes cerrado:

1. identificar las transacciones afectadas;
2. comparar categoría anterior vs nueva;
3. cuantificar el impacto;
4. revisar P&L, Cash Flow y Balance Sheet;
5. informar al usuario antes de considerar válido el cambio.

---

# Controles posteriores relevantes

Si se modifica una categoría con impacto financiero, revisar:

## P&L

- ingresos;
- gastos;
- EBITDA;
- resultado neto.

## Cash Flow

- cash operativo;
- financiamiento;
- caja final.

## Balance Sheet

- cash;
- CxC;
- CxP;
- retained earnings.

## Dashboard

- checks del modelo;
- cierre mensual;
- KPIs.

---

# Regla de materialidad

Una diferencia pequeña no autoriza automáticamente un cambio.

Nunca modificar categorías únicamente para eliminar:

- centavos;
- residuos de redondeo;
- diferencias de motor Excel vs Google Sheets.

Identificar primero la causa.

---

# Checklist rápido

Antes de modificar un catálogo:

- [ ] Leí `Config` en vivo.
- [ ] Busqué duplicados y variantes.
- [ ] Revisé reglas relacionadas.
- [ ] Revisé movimientos históricos.
- [ ] Confirmé que el cambio es necesario.
- [ ] No estoy usando categorización para modificar devengo.

Después de modificar:

- [ ] Releí la celda modificada.
- [ ] Validé reglas relacionadas.
- [ ] Revisé movimientos afectados.
- [ ] Revisé históricos cerrados.
- [ ] Revisé errores de fórmula.
- [ ] Revisé estados financieros si correspondía.
- [ ] Confirmé el resultado real antes de reportar terminado.

---

# Principio final

Los catálogos deben cambiar lentamente.

Una buena taxonomía financiera debe ser:

- estable;
- consistente;
- reutilizable;
- suficientemente granular;
- fácil de auditar.

Agregar categorías constantemente suele indicar que se está utilizando la categoría para almacenar información que debería vivir en:

- descripción;
- proyecto;
- responsable;
- proveedor;
- detalle documental.
