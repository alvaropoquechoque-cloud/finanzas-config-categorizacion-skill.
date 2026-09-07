---
name: finanzas-config-categorizacion
description: Mantiene los catálogos, validaciones y reglas automáticas de categorización del workflow financiero de Sommos.
---

# Finanzas Sommos — Config y Categorización

## Propósito

Administrar la configuración maestra y las reglas automáticas de categorización del modelo financiero de Sommos.

Esta skill define cómo se clasifican las transacciones, pero no registra movimientos bancarios, no concilia bancos y no calcula el tipo de cambio.

## Fuente principal

Google Sheet:

- Nombre: `Finanzas Sommos — Workflow y Control`
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

Pestañas principales de esta skill:

- `Config`
- `Reglas categorización`

Puede consultar `Transacciones` para validar cómo se está aplicando una regla.

## Principio de fuente viva

El Google Sheet es la fuente de verdad.

Los archivos dentro de `references/` documentan la lógica conocida, pero si existe una diferencia entre una referencia de GitHub y el Sheet actual, prevalece el Sheet.

Antes de modificar categorías o reglas, leer siempre la configuración vigente.

## Config

`Config` contiene las listas maestras utilizadas por el workflow financiero.

Entre ellas:

- países;
- monedas;
- tipos de transacción;
- áreas;
- categorías;
- estados de conciliación;
- valores Sí/No;
- proyectos/clientes;
- estados de CxC;
- estados de CxP;
- estados de presupuesto;
- estados de pago;
- cuentas y medios.

No agregar un valor a una transacción si ese valor requiere validación y todavía no existe en `Config`.

Cuando sea necesario crear una nueva categoría, cuenta, país, moneda o estado:

1. verificar que no exista ya;
2. confirmar que el nuevo valor sea realmente necesario;
3. agregarlo primero al catálogo correspondiente;
4. recién después utilizarlo en las demás pestañas.

## Tipos de transacción

Los tipos vigentes conocidos son:

- `Ingreso`
- `Egreso`
- `Transferencia interna`

No convertir una transferencia interna en ingreso o egreso únicamente para hacer cuadrar una conciliación.

## Reglas de categorización

La pestaña `Reglas categorización` utiliza principalmente:

- Palabra / frase
- Tipo
- Categoría
- Activa
- Responsable opcional
- Moneda opcional

La primera coincidencia activa válida es la que debe utilizar `Transacciones`.

Por lo tanto, el orden de las reglas importa.

Antes de insertar una nueva regla:

1. buscar reglas existentes con palabras equivalentes o similares;
2. revisar si una regla más general podría capturar el movimiento antes;
3. validar que la categoría exista en `Config`;
4. evitar duplicados;
5. colocar la regla en una posición coherente con su nivel de especificidad.

## Coincidencias opcionales

Una regla puede restringirse adicionalmente por:

- Responsable
- Moneda

Esto permite diferenciar movimientos con descripciones similares.

Ejemplo documentado:

`Hugo Christian`

puede clasificarse de forma diferente dependiendo de si el movimiento está en BOB o USD.

No eliminar estas restricciones al simplificar reglas.

## Transferencias internas

Los movimientos de tipo `Transferencia interna` deben clasificarse como:

`Transferencias internas`

Ejemplos conocidos:

- movimientos entre cuentas propias;
- pagos de tarjeta desde otra cuenta propia;
- `Brex Card Payment`;
- transferencias internas identificadas durante conciliación.

Una transferencia interna:

- no es ingreso operativo;
- no es gasto operativo;
- no debe aumentar ingresos;
- no debe aumentar burn;
- debe conservar cuenta origen y cuenta destino cuando se conozcan.

## Grants y financiamiento

Ingresos asociados a grants conocidos como:

- INNOVATECH
- Startup Perú
- INCOFIN
- FIID Guatemala

se clasifican como:

`Other financing cash flow`

No deben clasificarse automáticamente como ingreso operativo ordinario.

## Préstamos de accionistas

Los préstamos recibidos de accionistas se clasifican como:

`Shareholder loan received (non-interest)`

Las devoluciones de principal se clasifican como:

`Shareholder loan repayment (non-interest)`

El principal de un préstamo no debe confundirse con ingreso operativo ni con gasto operativo.

## Ingresos extraordinarios

Los ingresos identificados explícitamente como extraordinarios pueden utilizar:

`Ingresos extraordinarios`

No utilizar esta categoría como fallback genérico.

## Fallback de categorización

Si ninguna regla válida coincide, utilizar:

`Por categorizar`

Nunca inventar silenciosamente una categoría para evitar `Por categorizar`.

Si existe suficiente información para definir una nueva regla:

1. proponer o crear la regla;
2. validar su categoría;
3. comprobar posibles conflictos;
4. volver a revisar las transacciones afectadas.

## Modificación de reglas existentes

Cambiar una regla puede afectar transacciones futuras y también la interpretación de movimientos existentes.

Antes de editar una regla existente:

- identificar qué descripciones puede capturar;
- revisar si existen movimientos históricos relacionados;
- evitar reclasificaciones masivas no solicitadas;
- confirmar especialmente cambios entre ingresos, gastos, transferencias, financiamiento y salarios.

No modificar categorías históricas ya revisadas por el usuario únicamente porque una regla automática nueva produciría otro resultado.

## Flujo recomendado

Al recibir una descripción nueva o detectar una transacción sin clasificación:

1. leer `Config`;
2. leer las reglas activas relevantes;
3. comprobar si ya existe una coincidencia;
4. revisar Tipo, Responsable y Moneda;
5. validar la categoría;
6. crear o ajustar la regla únicamente si es necesario;
7. comprobar el resultado en `Transacciones`;
8. buscar conflictos o movimientos inesperadamente afectados.

## Reglas de seguridad

- No asumir posiciones históricas de columnas; leer encabezados actuales.
- No crear categorías duplicadas.
- No inventar países, monedas, responsables o cuentas.
- No cambiar `Ingreso`, `Egreso` y `Transferencia interna` sin evidencia.
- No utilizar una categoría de financiamiento como ingreso operativo.
- No utilizar transferencias internas como gasto o ingreso.
- No reclasificar movimientos históricos revisados sin una razón clara.
- Si una descripción es ambigua, conservar `Por categorizar` hasta resolverla.
- Después de modificar reglas, revisar las transacciones afectadas.
- Si el Sheet contradice una referencia estática de GitHub, prevalece el Sheet.

## Referencias

Consultar cuando sea necesario:

- `references/catalogos-y-validaciones.md`
- `references/reglas-conocidas.md`
