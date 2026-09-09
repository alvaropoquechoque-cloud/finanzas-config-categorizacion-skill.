# Finanzas Sommos — Reglas conocidas de categorización

## Propósito

Este documento registra patrones y casos conocidos del workflow financiero de Sommos.

Complementa:

`finanzas-config-categorizacion`

No reemplaza la pestaña viva:

`Reglas categorización`

La tabla del Google Sheet es siempre la fuente de verdad sobre:

- reglas existentes;
- orden;
- estado activa/inactiva;
- categorías destino.

Este documento sirve principalmente para:

- recordar casos especiales;
- evitar errores ya detectados;
- orientar la creación de nuevas reglas;
- preservar decisiones contables conocidas.

---

# Principio principal

Una regla automática debe utilizarse solamente cuando exista suficiente confianza de que el patrón identifica correctamente la naturaleza económica del movimiento.

Ante duda:

`Por categorizar`

es preferible a una clasificación incorrecta.

---

# Orden de prioridad

La regla más específica debe aparecer antes que la más genérica.

Ejemplo:

Correcto:

1. `GOOGLE CLOUD`
2. `GOOGLE`

Incorrecto:

1. `GOOGLE`
2. `GOOGLE CLOUD`

La segunda estructura puede provocar que la regla genérica capture movimientos que pertenecen a otra categoría.

---

# Antes de agregar una regla

Siempre:

1. buscar el texto en `Transacciones`;
2. revisar todas las coincidencias históricas;
3. comprobar Tipo;
4. revisar categorías actuales;
5. revisar Proyecto/Responsable;
6. comprobar reglas parecidas;
7. evaluar posibles falsos positivos;
8. colocar la regla en la prioridad correcta.

Nunca agregar una regla solamente mirando una única transacción.

---

# LARA / Caja Rural Los Andes

Este es un caso conocido de variación en la descripción bancaria.

Un patrón utilizado para identificar movimientos relacionados puede considerar:

`CAJA RURAL DE AHORRO Y CREDITO LOS`

o:

`LARA`

Ejemplo conceptual de regex:

`(?i)CAJA RURAL DE AHORRO Y CREDITO LOS|LARA`

Antes de modificar este patrón:

- revisar transacciones históricas;
- confirmar que no capture movimientos de terceros;
- preservar los cobros históricos correctamente identificados.

---

# PPO

PPO es un proveedor conocido.

Su gasto económico corresponde normalmente a:

`Outsourced services`

No crear una categoría llamada PPO únicamente por ser un proveedor.

PPO debe identificarse por:

- descripción;
- proveedor;
- detalle de factura;

mientras la categoría representa:

`Outsourced services`

## Caso especial PPO

Pueden existir varias facturas pagadas en un único movimiento bancario.

En esos casos:

- no asumir que el movimiento consolidado corresponde a un único mes;
- preservar la separación documental por factura;
- el devengo pertenece al mes de la factura;
- el pago pertenece al mes efectivo de cash.

La categorización no debe modificar esta lógica.

---

# Big Picture

Big Picture corresponde normalmente a:

`Outsourced services`

No confundir:

- proveedor;
- categoría económica.

Puede existir detalle adicional asociado a servicios legales o corporativos.

Clasificar según la naturaleza del servicio documentado.

---

# Endeavor

Caso histórico validado:

`Endeavor`

corresponde a:

`Outsourced services`

No clasificar automáticamente como:

- Administrative expenses;
- Marketing services;

sin evidencia de que el concepto haya cambiado.

---

# Google Cloud

Los movimientos claramente identificados como:

`GOOGLE CLOUD`

deben mantenerse separados de otros productos Google.

La clasificación económica conocida corresponde al costo tecnológico/plataforma utilizado por el modelo.

Categoría esperada:

`Platform cost`

cuando el movimiento corresponde efectivamente al servicio cloud.

Una regla genérica `GOOGLE` no debe capturar Google Cloud antes de esta regla.

---

# Google Workspace

Google Workspace no debe confundirse automáticamente con Google Cloud.

Es un software/herramienta operativa diferente.

Antes de clasificar:

- revisar la descripción exacta;
- verificar la categoría viva correspondiente;
- no reutilizar `Platform cost` solo porque el proveedor sea Google.

---

# ChatGPT / OpenAI

Los cargos identificados como ChatGPT/OpenAI corresponden a herramientas/software utilizadas por la operación.

Usar la categoría configurada para el concepto correspondiente en el Sheet vivo.

No crear categorías:

- `ChatGPT`;
- `OpenAI`;

solo por nombre del proveedor si ya existe una categoría económica aplicable.

---

# Anthropic / Claude

Aplicar el mismo principio que para ChatGPT.

`Claude` o `Anthropic` identifica al proveedor/producto.

La categoría debe representar el concepto financiero configurado.

---

# Microsoft

Los cargos Microsoft deben clasificarse según el servicio real.

No asumir automáticamente una categoría solamente por el nombre Microsoft si existen distintos productos.

Buscar coincidencias históricas antes de ampliar una regla.

---

# GitHub

Los cargos GitHub deben clasificarse según el uso tecnológico/software existente en el catálogo.

No crear una categoría `GitHub` solamente por proveedor.

---

# Figma

Figma es un software conocido dentro de los gastos de Sommos.

Importante:

el mes de devengo y el mes del movimiento bancario pueden diferir.

La regla de categorización únicamente define la naturaleza del movimiento.

No debe alterar por sí misma el saldo de CxP o el devengo histórico.

---

# Freepik

Aplicar la categoría económica configurada para herramientas/software o el concepto vivo correspondiente.

No crear una categoría individual por proveedor.

---

# Udemy

Los movimientos Udemy deben clasificarse según la categoría económica que figure en el modelo vivo.

Revisar históricos antes de agregar patrones amplios.

---

# Innovatech — gasto

Existe una categoría específica:

`Innovatech`

para determinados gastos relacionados con el programa/proyecto.

No confundir estos egresos con los desembolsos de financiamiento del mismo nombre.

La combinación:

- Tipo;
- descripción;
- contexto;

es fundamental.

---

# INNOVATECH — grant / financiamiento

Un desembolso del programa INNOVATECH corresponde conceptualmente a:

`Other financing cash flow`

y no a la categoría de gasto:

`Innovatech`

Por lo tanto:

## Egreso relacionado con ejecución del proyecto

Puede corresponder a:

`Innovatech`

## Ingreso/desembolso del financiamiento

Corresponde normalmente a:

`Other financing cash flow`

No utilizar una única regla de texto sin considerar Tipo.

---

# Startup Perú

Los desembolsos de Startup Perú corresponden a financiamiento/grant.

Categoría:

`Other financing cash flow`

Caso conocido 2026:

existió un desembolso programado/cobrado de aproximadamente:

`USD 934`

en septiembre.

Esta partida debe mantenerse separada de ingreso operativo.

---

# INCOFIN

INCOFIN corresponde a financiamiento/grant.

Categoría esperada:

`Other financing cash flow`

No clasificar como:

- ingresos operativos;
- Others de P&L;

sin una decisión contable explícita.

---

# FIID Guatemala

FIID Guatemala corresponde a financiamiento/grant.

Categoría esperada:

`Other financing cash flow`

Preservar la separación entre:

- aprobación;
- desembolso programado;
- cobro;
- saldo.

---

# Bank fees

Descripciones que representen comisiones bancarias deben utilizar:

`Bank fees`

No incluir dentro de esta regla:

- intereses;
- diferencias de cambio;
- impuestos;
- transferencias;
- financiamiento.

Una palabra como:

`COMISION`

puede ser demasiado genérica.

Revisar contexto/banco antes de crear una regla amplia.

---

# Interés bancario ganado

Cuando el banco acredita intereses a favor de Sommos:

Categoría:

`Bank interest earned`

No confundir con:

`Other financing cash flow`

ni con ingreso operativo.

---

# Gasto financiero / interés pagado

Intereses pagados o devengados relacionados con financiamiento deben utilizar:

`Financial expense`

cuando corresponda.

No utilizar:

`Bank fees`

solo porque el movimiento provenga de una institución financiera.

---

# Exchange rate differences

Diferencias de cambio deben utilizar:

`Exchange rate differences`

cuando representan efecto cambiario y no un pago operativo.

No utilizar esta categoría para cualquier conversión de moneda.

Debe existir una diferencia económica/cambiaria real.

---

# Transferencias internas

Las transferencias entre cuentas propias deben identificarse como:

Tipo:

`Transferencia interna`

Categoría:

`Transferencias internas`

No deben entrar en:

- ingresos;
- gastos;
- CxC;
- CxP;
- P&L.

Sí deben afectar los saldos de las cuentas bancarias correspondientes.

---

# Impuestos

Impuestos como IVA/IT u otros conceptos fiscales deben mantenerse separados de:

- Bank fees;
- Administrative expenses;
- Financial expense.

Utilizar la categoría fiscal definida en `Config`.

Cuando el modelo utilice una línea específica:

`Taxes`

respetar su mapeo contable.

---

# Viajes

Los movimientos de viaje deben clasificarse según el concepto real.

Una categoría conocida es:

`Travel`

Pero algunos gastos pueden pertenecer específicamente a:

`Innovatech`

dependiendo del proyecto.

Utilizar Proyecto/Responsable cuando ayude a distinguirlos.

---

# Marketing

Servicios de marketing pueden utilizar:

`Marketing services`

No asumir que cualquier gasto publicitario o creativo pertenece a esta categoría sin revisar el concepto.

---

# Nómina

Las categorías relacionadas con salarios pueden incluir:

- `IT salaries`
- `Operative salaries`
- `Finance Salary`
- `RH Salary`
- `Sales salaries`

Las reglas bancarias pueden ayudar a clasificar pagos.

Pero:

**la categorización del pago no define el devengo salarial.**

El devengo viene de:

`Sueldos 2026`

y el saldo se controla en:

`CxP Sueldos`

---

# Otros / Others

Usar `Others` con cuidado.

No utilizarlo como categoría por defecto para evitar:

`Por categorizar`

`Others` debe representar realmente un concepto residual previsto por el modelo.

Si el movimiento no es entendible:

mantener `Por categorizar`.

---

# Palabras demasiado genéricas

Evitar reglas basadas únicamente en términos como:

- PAGO
- TRANSFERENCIA
- SERVICIO
- COMPRA
- COMISION
- GOOGLE
- BANCO
- COBRO
- DEBITO
- CREDITO

Estas palabras pueden generar demasiados falsos positivos.

---

# Uso de regex

Cuando varias variantes representan inequívocamente el mismo concepto, puede utilizarse un patrón regex.

Ejemplo conocido:

`(?i)CAJA RURAL DE AHORRO Y CREDITO LOS|LARA`

Reglas:

- mantener patrones legibles;
- evitar regex excesivamente amplios;
- comprobar todas las coincidencias históricas;
- escapar caracteres especiales cuando corresponda;
- documentar casos no evidentes.

---

# Reglas específicas por Tipo

Cuando una misma palabra pueda representar tanto un ingreso como un egreso:

crear reglas diferenciadas por Tipo.

Ejemplo:

`INNOVATECH`

puede representar:

- un gasto de proyecto;
- un desembolso de grant.

La palabra sola no es suficiente.

---

# Reglas específicas por Proyecto

Cuando dos movimientos con descripción similar pertenezcan a contextos distintos:

utilizar Proyecto/Cliente o Responsable si la tabla viva lo permite.

Esto es preferible a fragmentar innecesariamente las categorías.

---

# Protección de históricos

Antes de modificar una regla que ya existe:

1. identificar todas las transacciones históricas que coincide;
2. revisar especialmente meses cerrados;
3. comparar categoría actual vs propuesta;
4. cuantificar el impacto;
5. revisar P&L si el cambio es material.

No asumir que una regla nueva es mejor solo porque sea más específica.

---

# Agosto 2026

Agosto de 2026 se considera actualmente un mes cerrado y conciliado dentro del workflow financiero.

Una modificación de regla que cambie movimientos de agosto debe tratarse como una modificación de histórico.

No aplicar silenciosamente.

---

# Validación después de cambiar una regla

Después de modificar o crear una regla:

1. releer `Reglas categorización`;
2. comprobar que quedó en el orden correcto;
3. revisar ejemplos que deberían coincidir;
4. revisar ejemplos que no deberían coincidir;
5. comprobar `Transacciones`;
6. revisar el contador `Por categorizar`;
7. revisar movimientos del último mes cerrado;
8. buscar errores de fórmula.

Si afecta categorías financieras materiales, revisar además:

- `Real P&L`
- `Cash Flow`
- `Balance Sheet`
- `Dashboard`

---

# Casos que nunca deben resolverse automáticamente

No automatizar sin suficiente evidencia:

- proveedores con múltiples tipos de servicio;
- movimientos con descripción genérica;
- transferencias que podrían ser internas o externas;
- devoluciones;
- reembolsos;
- préstamos;
- aportes de accionistas;
- movimientos fiscales ambiguos;
- movimientos con moneda o banco desconocido.

Mantener:

`Por categorizar`

hasta obtener contexto.

---

# Regla final

Una buena regla de categorización debe ser:

- específica;
- explicable;
- repetible;
- estable;
- auditable.

El objetivo no es maximizar el porcentaje de categorización automática.

El objetivo es maximizar la **categorización automática correcta**.
