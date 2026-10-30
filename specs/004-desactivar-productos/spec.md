# Spec 004: Desactivar productos

## Objetivo

Permitir que un empleado marque un producto como inactivo sin borrar sus datos ni su historial.

## Actores

- Empleado: persona autorizada para mantener el catálogo.

## Reglas de negocio

- La desactivación es lógica: el registro y sus movimientos se conservan.
- Un producto inactivo no se ofrece en el catálogo normal ni se puede seleccionar para nuevos pedidos.
- La desactivación no cambia el stock ni altera facturas, pedidos o movimientos anteriores.
- No se permite volver a registrar el mismo código; los códigos siguen siendo únicos incluso para productos inactivos.

## Historias de usuario

- HU-1: Como empleado, quiero desactivar un producto que ya no se vende, para retirarlo del catálogo sin perder su historial.
- HU-2: Como empleado, quiero recibir confirmación del resultado, para saber si el producto quedó inactivo.

## Criterios de aceptación

- CA-1: Dado un producto activo, cuando el empleado solicita desactivarlo, el sistema lo marca inactivo y confirma la operación.
- CA-2: La operación conserva todos los datos y el historial de inventario del producto.
- CA-3: Si el código no existe, el sistema informa que el producto no fue encontrado y no cambia datos.
- CA-4: Si el producto ya está inactivo, el sistema informa que no se realizó ningún cambio.
- CA-5: Después de desactivarlo, el producto no puede agregarse a un pedido nuevo.

## Casos límite

- Una desactivación repetida no crea estados o movimientos adicionales.
- Una solicitud fallida no debe cambiar parcialmente el estado del producto.
- Un producto con stock disponible puede desactivarse; su stock se conserva para consulta e historial.

## Fuera de alcance

- Borrar físicamente el producto
- Reactivar productos
- Ajustar o retirar el stock existente
- Cancelar pedidos o facturas históricas
