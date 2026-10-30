# Spec 010: Registrar salida y ajuste de inventario

## Objetivo

Permitir que un empleado registre salidas o correcciones justificadas de stock, preservando la trazabilidad y prohibiendo stock negativo.

## Actores

- Empleado: persona autorizada para gestionar inventario.

## Datos del movimiento

| Dato | Obligatorio | Regla |
|---|---|---|
| Producto | Sí | Producto existente |
| Tipo | Sí | Salida o ajuste |
| Cantidad | Sí | Entero mayor que cero para salida; entero distinto de cero para ajuste |
| Motivo | Sí | Texto no vacío de hasta 250 caracteres |

Una salida disminuye el stock por la cantidad indicada. Un ajuste representa una variación: positiva aumenta el stock y negativa lo disminuye. Todo movimiento conserva stock anterior y resultante, tipo, cantidad o variación, motivo y fecha UTC.

## Historias de usuario

- HU-1: Como empleado, quiero registrar una salida, para reflejar mercancía retirada del inventario.
- HU-2: Como empleado, quiero ajustar una diferencia de stock con un motivo, para corregir el inventario de forma auditable.
- HU-3: Como empleado, quiero que el sistema impida un stock negativo, para evitar inconsistencias.

## Criterios de aceptación

- CA-1: Una salida válida disminuye el stock y registra el movimiento en una sola operación atómica.
- CA-2: Un ajuste válido aplica la variación indicada y registra el motivo y los stocks anterior y resultante.
- CA-3: Si el resultado sería negativo, el sistema rechaza la operación y no registra movimiento.
- CA-4: Un ajuste de cero se rechaza porque no representa un cambio.
- CA-5: Si el producto no existe, el sistema rechaza la operación sin cambios.
- CA-6: Si falta el motivo o el tipo, o la cantidad es inválida, el sistema informa el error y no modifica stock.
- CA-7: El stock y el movimiento se confirman juntos o ninguno se guarda.
- CA-8: Una factura emitida registra su propio movimiento de salida asociado, sin permitir duplicar la salida desde esta funcionalidad.

## Casos límite

- El sistema valida el stock y aplica el cambio de forma atómica ante solicitudes simultáneas.
- Un producto inactivo puede recibir un ajuste correctivo o una salida para conservar la exactitud de su inventario, pero no puede volver a venderse.
- Un movimiento fallido no altera el historial.

## Fuera de alcance

- Registrar entradas
- Cambiar manualmente el stock sin crear movimiento
- Anular facturas o devolver stock por una anulación
- Borrar o editar movimientos históricos
