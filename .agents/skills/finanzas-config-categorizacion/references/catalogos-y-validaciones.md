# Catálogos y validaciones

Validaciones conocidas en `Transacciones`:
- Tipo → Config
- País → Config
- Categoría → Config
- Moneda → Config
- Cuenta / medio → Config
- Conciliación → Config
- Presupuestado → Config
- Estado pago → Config

Valores clave:
- Estado pago: `Pagado/Cobrado` o `Pendiente`
- Conciliación incluye estados como `Conciliado` y `Pendiente`
- Categoría de fallback: `Por categorizar`

No añadir valores nuevos solo para resolver un caso puntual sin validar que representan una dimensión reutilizable.
