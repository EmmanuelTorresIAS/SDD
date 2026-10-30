# Spec 007: Editar clientes

## Objetivo

Permitir que un empleado actualice los datos de identificación y contacto de un cliente existente.

## Actores

- Empleado: persona autorizada para mantener los datos de clientes.

## Reglas de negocio

- Se pueden modificar el tipo y número de identificación, nombre o razón social, teléfono y correo.
- Se aplican las reglas de validación de [005-registrar-clientes](../005-registrar-clientes/spec.md).
- La identificación actualizada debe seguir siendo única en el sistema.
- El registro de cambios no altera pedidos ni facturas emitidos anteriormente.

## Historias de usuario

- HU-1: Como empleado, quiero corregir los datos de un cliente, para mantener información actualizada.
- HU-2: Como empleado, quiero que el sistema impida identificaciones duplicadas, para preservar la unicidad.

## Criterios de aceptación

- CA-1: Al guardar datos válidos para un cliente existente, el sistema actualiza los datos y confirma el resultado.
- CA-2: Si una identificación nueva ya pertenece a otro cliente, el sistema rechaza el cambio sin modificar ningún dato.
- CA-3: Si algún dato incumple su regla, el sistema informa todos los errores y no guarda cambios parciales.
- CA-4: Si el cliente no existe, el sistema informa que no fue encontrado.
- CA-5: Si el cliente está inactivo, el sistema rechaza la edición.
- CA-6: Si la identificación no cambia, no se considera un duplicado de sí misma.

## Casos límite

- Se eliminan espacios al inicio y al final antes de validar y guardar.
- Si dos empleados actualizan simultáneamente el mismo cliente, el sistema informa el conflicto en lugar de sobrescribir silenciosamente cambios.
- Las referencias históricas conservan la identidad del cliente asociado.

## Fuera de alcance

- Desactivar o reactivar clientes
- Eliminar clientes
- Modificar pedidos o facturas existentes
- Mantener una auditoría detallada de cada valor anterior y nuevo
