# Spec 011: Consultar stock y movimientos

## Objetivo

Permitir que un empleado consulte el stock actual de un producto y el historial de movimientos que lo explica.

## Actores

- Empleado: persona que consulta la disponibilidad y trazabilidad de mercancía.

## Reglas de consulta

- La consulta se realiza para un producto identificado por su código.
- El resultado incluye código y nombre del producto, estado, stock actual y movimientos ordenados del más reciente al más antiguo.
- Cada movimiento muestra tipo, cantidad o variación, stock anterior y resultante, motivo o referencia, fecha UTC y empleado cuando esté disponible.
- El historial se pagina para permitir consultas extensas.
- Los productos inactivos siguen disponibles para consulta histórica.

## Historias de usuario

- HU-1: Como empleado, quiero consultar el stock actual, para saber cuántas unidades están disponibles.
- HU-2: Como empleado, quiero revisar los movimientos, para entender cómo cambió el stock.

## Criterios de aceptación

- CA-1: Para un producto existente, el sistema devuelve el stock actual y sus movimientos en orden cronológico inverso.
- CA-2: Los movimientos paginados no se repiten ni se omiten entre páginas mientras el historial no cambie.
- CA-3: Si el producto existe y nunca tuvo movimientos, el stock se muestra en cero y el historial vacío.
- CA-4: Si el código no existe, el sistema informa que el producto no fue encontrado.
- CA-5: La consulta no modifica stock ni movimientos.

## Casos límite

- El historial de un producto inactivo sigue siendo consultable.
- Los movimientos con igual fecha mantienen un orden estable.
- El stock mostrado corresponde al valor actual, no a una suma calculada solo con la página solicitada.

## Fuera de alcance

- Modificar stock o movimientos
- Consultar el inventario de todos los productos en una sola vista
- Exportar el historial
- Mostrar valorización financiera del inventario
