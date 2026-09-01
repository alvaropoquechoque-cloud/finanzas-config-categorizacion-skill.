---
name: finanzas-config-categorizacion
description: Mantiene catálogos y reglas automáticas de categorización del workflow financiero de Sommos.
---

# Finanzas Sommos — Config y Categorización

## Propósito

Administrar la base estructural del modelo financiero: catálogos, listas válidas y reglas que determinan cómo se clasifican las transacciones.

Archivo principal:
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

## Alcance

Esta skill opera principalmente:
- `Config`
- `Reglas categorización`

Puede leer `Transacciones` para verificar el efecto de las reglas, pero no debe usar esta skill como mecanismo principal para registrar movimientos financieros.

## Responsabilidades

1. Mantener países, monedas, cuentas/medios, estados, opciones booleanas y categorías válidas.
2. Crear o ajustar reglas por palabra/frase, tipo, responsable opcional y moneda opcional.
3. Respetar el principio de primera coincidencia activa.
4. Validar que una nueva categoría exista en `Config` antes de usarla en una regla.
5. Revisar filas `Por categorizar` para proponer reglas, sin reasignar silenciosamente categorías dudosas.
6. No eliminar valores de catálogos sin revisar todas sus dependencias.

## Regla de categorización

La categoría de `Transacciones` se deriva de las reglas. Ejemplos conocidos:
- Google Cloud → Platform cost
- ChatGPT → Softwares for development
- Microsoft → Platform cost
- PPO → Outsourced services
- IVA Sommos → Taxes
- Interest on Convertible Notes → Financial expense
- grants identificados → Other financing cash flow

Si no hay coincidencia segura, mantener `Por categorizar`.

## Reglas transversales obligatorias

- El Google Sheet `Finanzas Sommos — Workflow y Control` es la fuente viva.
- `Transacciones` es la fuente de verdad operativa para movimientos realizados y pendientes.
- Antes de escribir, leer en vivo encabezados, fórmulas, validaciones y filas relacionadas.
- Nunca asumir posiciones históricas de columnas.
- Nunca duplicar una transacción existente.
- Nunca inventar país, categoría, responsable, fecha de vencimiento, cuenta o medio.
- Si no existe una categoría válida, usar `Por categorizar` hasta que se defina una regla.
- `Pendiente` no equivale a dinero realizado ni debe afectar bancos/caja.
- Después de cualquier modificación, verificar las vistas dependientes y buscar errores de fórmula.
- Los snapshots en GitHub documentan contexto; si contradicen el Sheet, prevalece el Sheet.
