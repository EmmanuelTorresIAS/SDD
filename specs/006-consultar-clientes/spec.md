# Spec 006: Consultar clientes

## Objetivo

Permitir que un empleado liste clientes y consulte el detalle de uno para gestionarlo o asociarlo a un pedido.

## Actores

- Empleado: persona que administra clientes y ventas.

## Reglas de consulta

- El listado muestra clientes activos por defecto, paginados y ordenados por nombre o razón social.
- El detalle incluye tipo y número de identificación, nombre o razón social, teléfono, correo, estado y fecha de creación.
- Un cliente inactivo no aparece en el listado normal; su detalle puede consultarse e indica claramente el estado.
- Esta consulta no modifica datos del cliente.

## Historias de usuario

- HU-1: Como empleado, quiero listar clientes activos, para localizar a quién asociar una venta.
- HU-2: Como empleado, quiero ver el detalle de un cliente, para confirmar sus datos de identificación y contacto.

## Criterios de aceptación

- CA-1: Sin filtros, el sistema devuelve clientes activos ordenados por nombre o razón social.
- CA-2: Los resultados se pueden recorrer por páginas sin repetir ni omitir registros mientras los datos no cambien.
- CA-3: Al consultar una identificación existente, el sistema muestra todos los datos definidos para el detalle.
- CA-4: Si no existe la identificación, el sistema informa que el cliente no fue encontrado.
- CA-5: Si el cliente está inactivo, el detalle lo indica explícitamente.
- CA-6: Un listado sin resultados se devuelve vacío, no como error.

## Casos límite

- Los campos opcionales no informados se muestran vacíos.
- La identificación se consulta sin distinguir mayúsculas y minúsculas.
- Una consulta fallida no modifica los datos.

## Fuera de alcance

- Crear, editar o desactivar clientes
- Búsqueda avanzada o exportación de resultados
- Consultar pedidos o facturas desde el detalle del cliente
