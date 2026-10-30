# Spec 003: Editar productos

## Objetivo

Permitir que un empleado corrija o actualice los datos de un producto sin cambiar su código.

## Actores

- Empleado: persona autorizada para mantener el catálogo.

## Datos editables

Se aplican las mismas reglas de longitud, obligatoriedad y precio definidas en [001-registrar-productos](../001-registrar-productos/spec.md). Se pueden modificar nombre, categoría, precio de venta, talla y color. El código no se puede modificar.

## Historias de usuario

- HU-1: Como empleado, quiero actualizar los datos de un producto, para mantener el catálogo correcto.
- HU-2: Como empleado, quiero que el sistema valide los datos actualizados, para evitar información inválida.

## Criterios de aceptación

- CA-1: Dado un producto existente y activo, cuando el empleado guarda cambios válidos, el sistema actualiza los campos enviados y confirma el resultado.
- CA-2: El código del producto permanece sin cambios y no puede incluirse como dato editable.
- CA-3: Los campos obligatorios no pueden quedar vacíos y el precio debe ser mayor que cero.
- CA-4: Si uno o más valores incumplen las reglas, el sistema informa todos los errores y no guarda ningún cambio.
- CA-5: Si el código no corresponde a un producto, el sistema informa que no fue encontrado.
- CA-6: Si el producto está inactivo, el sistema rechaza la edición.
- CA-7: Editar un producto no cambia su stock ni modifica movimientos de inventario existentes.

## Casos límite

- Los espacios al inicio y al final se eliminan antes de validar y guardar, como en el registro.
- Un cambio rechazado conserva intactos todos los datos previos.
- Si dos empleados editan simultáneamente el mismo producto, el sistema no debe confirmar silenciosamente una actualización que sobrescriba cambios ajenos; informa el conflicto para que se vuelva a consultar el producto.

## Fuera de alcance

- Cambiar el código
- Activar o desactivar productos
- Registrar o ajustar stock
- Editar movimientos históricos
