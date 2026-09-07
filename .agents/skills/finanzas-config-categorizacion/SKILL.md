---
name: finanzas-config-categorizacion
description: Mantiene los catálogos, validaciones y reglas automáticas de categorización del modelo financiero de Sommos.
---

# Finanzas Sommos — Config y Categorización

## Objetivo

Mantener consistente la estructura maestra del modelo financiero de Sommos antes de registrar, importar o analizar movimientos.

Esta skill es responsable de:

- `Config`
- `Reglas categorización`

Puede consultar `Transacciones` para validar el efecto de las reglas, pero no es responsable de registrar movimientos bancarios, CxC, CxP, presupuesto, conciliación o runway.

## Fuente de verdad

Google Sheet:

- Nombre: `Finanzas Sommos — Workflow y Control`
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

El Google Sheet vivo siempre prevalece sobre snapshots, ejemplos o documentación guardada en GitHub.

Antes de modificar algo, leer en vivo las pestañas y rangos afectados.

## Cuándo usar esta skill

Usar esta skill cuando sea necesario:

- crear o modificar una categoría;
- añadir un país;
- añadir una moneda;
- añadir una cuenta o medio bancario;
- modificar tipos de transacción;
- modificar estados de pago;
- crear, activar, desactivar o corregir reglas de categorización;
- investigar por qué una transacción quedó mal categorizada;
- revisar movimientos `Por categorizar`;
- validar que una categoría utilizada en `Transacciones` exista en `Config`.

## Catálogos actuales

Los catálogos deben leerse siempre desde `Config`.

Valores conocidos actualmente incluyen:

### Países

- BOLIVIA
- USA
- PERU
- CHILE
- GUATEMALA

### Monedas

- BOB
- USD
- SOL
- CLP

### Tipos de transacción

- `Ingreso`
- `Egreso`
- `Transferencia interna`

`Transferencia interna` es el nombre canónico actual.

No crear variantes como `Transferencia`, `Transfer`, `Traspaso` u otras sin modificar primero el modelo de manera controlada.

### Bancos / medios conocidos

- Banco Sol
- Brex
- Brex Card
- Meru
- Scotiabank
- BCI

Siempre validar la lista viva antes de añadir otro valor.

## Categorías

Las categorías válidas se administran en `Config`.

Entre las categorías actualmente utilizadas se encuentran:

- Outsourced services
- RH expenses
- Administrative expenses
- Sales expenses
- Travel
- Product expenses
- Softwares for development
- Innovatech
- Platform cost
- Bank fees
- Exchange rate differences
- Financial expense
- Taxes
- Startup Chile
- Marketing services
- Contingency
- Full new integration incomes
- Extra features development income
- Proof of concept incomes
- IT salaries
- Sales salaries
- Finance salaries
- Operative salaries
- RH salaries
- Transferencias internas
- Bank interest earned
- Other financing cash flow
- Shareholder loan received (non-interest)
- Shareholder loan repayment (non-interest)
- Ingresos extraordinarios
- Por categorizar

No asumir que esta lista es permanente.

Antes de asignar o crear una categoría, revisar `Config`.

## Reglas de categorización

La pestaña `Reglas categorización` contiene:

- Palabra/frase
- Tipo
- Categoría
- Activa
- Responsable opcional
- Moneda opcional

Las reglas se evalúan en orden.

La primera regla activa que cumple las condiciones es la que debe prevalecer.

## Procedimiento para crear o modificar una regla

1. Leer `Config`.
2. Leer `Reglas categorización`.
3. Confirmar que la categoría destino existe.
4. Buscar reglas similares o duplicadas.
5. Revisar si una regla anterior podría capturar el movimiento antes.
6. Usar la descripción o patrón más específico posible.
7. Aplicar `Tipo` cuando ayude a evitar falsos positivos.
8. Usar Responsable o Moneda solo cuando realmente sean necesarios.
9. Mantener `Activa = Sí` únicamente para reglas vigentes.
10. Probar la regla sobre transacciones existentes relacionadas.
11. Confirmar que no cambió accidentalmente la categorización de otros movimientos.

## Principio de especificidad

Preferir reglas específicas sobre reglas demasiado generales.

Ejemplo:

Una regla para `Banco Sol` + `Ingreso` puede ser válida para ingresos comerciales específicos, pero una regla genérica únicamente basada en la palabra `Banco` sería demasiado amplia.

No crear reglas que puedan capturar cargos bancarios, transferencias u otros conceptos no relacionados.

## Transferencias internas

Para movimientos entre cuentas propias:

- Tipo = `Transferencia interna`
- Categoría = `Transferencias internas`

La transferencia debe conservar además:

- Cuenta origen
- Cuenta destino

Las transferencias internas:

- no son ingreso operativo;
- no son gasto operativo;
- no forman parte del burn;
- no deben alterar el resultado financiero;
- sí deben afectar la conciliación de las cuentas origen y destino correspondientes.

## Categoría desconocida

Si no existe información suficiente para clasificar un movimiento:

`Por categorizar`

Nunca inventar silenciosamente una categoría.

Si el usuario posteriormente confirma la naturaleza del movimiento:

1. crear o ajustar la regla correspondiente si es reutilizable;
2. recategorizar el movimiento;
3. comprobar si existen otros movimientos similares;
4. verificar que no queden registros equivalentes como `Por categorizar`.

## Grants y financiamiento

No clasificar automáticamente un grant como ingreso operativo ordinario.

Los grants pueden utilizar:

`Other financing cash flow`

según la naturaleza registrada en el modelo.

Ejemplos conocidos:

- INNOVATECH
- Startup Perú
- INCOFIN
- FIID Guatemala

El monto total aprobado de un grant no equivale automáticamente a una cuenta por cobrar ni a ingreso realizado.

La categorización únicamente define la naturaleza del movimiento; el reconocimiento de CxC y caja pertenece a otras skills.

## Sueldos

Las categorías salariales deben conservar la separación funcional existente:

- IT salaries
- Sales salaries
- Finance salaries
- Operative salaries
- RH salaries

No consolidarlas en una única categoría `Salaries` dentro de `Transacciones` salvo que el modelo sea modificado explícitamente.

Las vistas de presupuesto pueden agruparlas posteriormente para reporting.

## Cambios en Config

Antes de añadir un nuevo valor a un catálogo:

1. comprobar que no exista con otro nombre;
2. evitar duplicados por mayúsculas, espacios o variantes;
3. revisar validaciones dependientes;
4. revisar fórmulas que comparen textos exactos;
5. comprobar reglas de categorización relacionadas.

No renombrar valores existentes sin investigar primero sus dependencias.

## Validaciones posteriores

Después de cualquier cambio:

1. volver a leer las filas modificadas;
2. comprobar que las validaciones sigan funcionando;
3. revisar transacciones relacionadas;
4. buscar `Por categorizar` inesperados;
5. buscar errores `#REF!`, `#VALUE!`, `#N/A` o `#ERROR!`;
6. confirmar que no se generaron categorías o reglas duplicadas.

## Límites de esta skill

Esta skill no debe:

- importar extractos bancarios;
- registrar movimientos en `Transacciones`;
- modificar tipos de cambio;
- conciliar bancos;
- crear CxC o CxP;
- modificar presupuesto;
- calcular runway;
- modificar directamente KPIs del Dashboard.

Cuando una solicitud pertenezca a esos procesos, usar la skill financiera correspondiente.

## Principio final

Configurar primero, registrar después.

Una buena categorización debe hacer que las siguientes capas del modelo —Transacciones, CxC, CxP, Real S&A, Operative incomes, Bancos, Runway y Dashboard— funcionen sin correcciones manuales innecesarias.
