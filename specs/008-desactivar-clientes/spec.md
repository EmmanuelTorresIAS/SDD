# Spec 008: Desactivar clientes

## Objetivo

Permitir que un empleado marque un cliente como inactivo sin borrar sus datos ni su historial comercial.

## Actores

- Empleado: persona autorizada para mantener el catálogo de clientes.

## Reglas de negocio

- La desactivación es lógica y conserva los datos y referencias históricas.
- Un cliente inactivo no se puede seleccionar para nuevos pedidos.
- La identificación de un cliente inactivo sigue reservada y no puede registrarse para otro cliente.
- La desactivación no cancela ni modifica pedidos o facturas existentes.

## Historias de usuario

- HU-1: Como empleado, quiero desactivar un cliente, para evitar nuevas operaciones con sus datos.
- HU-2: Como empleado, quiero conservar sus facturas y pedidos anteriores, para mantener la trazabilidad.

## Criterios de aceptación

- CA-1: Al desactivar un cliente activo, el sistema cambia su estado y confirma el resultado.
- CA-2: El sistema conserva los datos y documentos relacionados con el cliente.
- CA-3: Si el cliente no existe, el sistema informa que no fue encontrado.
- CA-4: Si el cliente ya está inactivo, el sistema informa que no realizó cambios.
- CA-5: Un cliente inactivo no puede asociarse a un pedido nuevo.

## Casos límite

- Las solicitudes repetidas no producen cambios adicionales.
- Una solicitud fallida no deja un estado parcialmente actualizado.
- Los documentos anteriores siguen siendo consultables con el cliente inactivo.

## Fuera de alcance

- Borrar datos de cliente
- Reactivar clientes
- Anular facturas o cancelar pedidos
