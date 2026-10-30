# Spec 009: Registrar entrada de inventario

## Objetivo

Permitir que un empleado registre la entrada de unidades de un producto y aumente su stock con un movimiento trazable.

## Actores

- Empleado: persona que recibe y controla mercancía.

## Datos del movimiento

| Dato | Obligatorio | Regla |
|---|---|---|
| Producto | Sí | Producto existente y activo |
| Cantidad | Sí | Número entero mayor que cero |
| Motivo o referencia | No | Texto de hasta 250 caracteres |

El sistema registra tipo de movimiento (entrada), cantidad, stock anterior, stock resultante, fecha y hora UTC, y empleado que lo realizó cuando su identidad esté disponible.

## Historias de usuario

- HU-1: Como empleado, quiero registrar unidades recibidas, para mantener actualizado el stock.
- HU-2: Como empleado, quiero que cada entrada deje un movimiento, para poder rastrear cambios de inventario.

## Criterios de aceptación

- CA-1: Dado un producto activo y una cantidad válida, el sistema incrementa el stock y registra el movimiento de forma atómica.
- CA-2: El movimiento conserva cantidad, tipo, producto, stock anterior y resultante, fecha de creación y referencia proporcionada.
- CA-3: Si el producto no existe o está inactivo, el sistema rechaza la operación sin modificar el stock.
- CA-4: Si la cantidad falta, no es entera o no es mayor que cero, el sistema rechaza la solicitud.
- CA-5: Si falla el registro del movimiento, el stock tampoco cambia; si falla el cambio de stock, no queda movimiento.
- CA-6: Una entrada válida nunca reduce el stock.

## Casos límite

- La cantidad no admite fracciones ni valores fuera del rango que el sistema pueda almacenar.
- Una operación repetida intencionalmente registra una nueva entrada; el sistema no la duplica sin una clave de idempotencia acordada.
- Un producto inactivo conserva su stock, pero no admite nuevas entradas por esta funcionalidad.

## Fuera de alcance

- Registrar salidas o ajustes
- Asociar automáticamente la entrada a un envío
- Consultar el historial completo
- Importar movimientos de forma masiva
