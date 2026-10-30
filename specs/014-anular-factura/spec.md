# Spec 014: Anular factura

## Objetivo

Permitir que un empleado anule una factura emitida y revierta el stock descontado, sin borrar el documento ni sus movimientos.

## Actores

- Empleado: persona autorizada para gestionar facturas.

## Reglas de negocio

- Solo se puede anular una factura emitida que no esté anulada.
- La anulación conserva la factura original, su número, datos y estado histórico.
- Cada unidad devuelta se registra como un movimiento de entrada asociado a la factura y a la anulación.
- La actualización del estado de factura, los movimientos de devolución y el aumento de stock ocurren en una sola transacción.
- Una factura anulada no se puede editar, volver a emitir ni anular otra vez.

## Historias de usuario

- HU-1: Como empleado, quiero anular una factura emitida, para corregir una venta cancelada.
- HU-2: Como empleado, quiero que el stock vendido se devuelva automáticamente, para mantener el inventario correcto.
- HU-3: Como empleado, quiero conservar la factura anulada y el motivo, para mantener la trazabilidad.

## Criterios de aceptación

- CA-1: Al anular una factura emitida con motivo válido, el sistema la marca anulada, conserva su número y devuelve las cantidades al stock.
- CA-2: La operación registra un movimiento de entrada por cada producto, vinculado a la factura y con el motivo de anulación.
- CA-3: Si falla la devolución de stock o el registro de un movimiento, ni la anulación ni ninguna devolución quedan aplicadas.
- CA-4: Si la factura no existe, ya está anulada o no está emitida, el sistema rechaza la operación sin cambios.
- CA-5: Una solicitud repetida no devuelve stock por segunda vez.
- CA-6: La anulación no libera ni reutiliza el número de factura.

## Casos límite

- La devolución puede aumentar el stock de un producto que entretanto fue desactivado; la trazabilidad histórica debe conservarse.
- Una anulación concurrente de la misma factura solo puede aplicarse una vez.
- El motivo de anulación es obligatorio y se conserva con la fecha UTC y el empleado cuando su identidad esté disponible.

## Fuera de alcance

- Borrar facturas
- Reutilizar números de factura
- Anulaciones parciales o devoluciones parciales
- Emitir notas crédito fiscales o comunicarse con la DIAN
