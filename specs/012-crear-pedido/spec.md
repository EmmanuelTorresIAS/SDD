# Spec 012: Crear pedido

## Objetivo

Permitir que un empleado prepare un pedido para un cliente con productos y cantidades, sin descontar stock ni emitir una factura.

## Actores

- Empleado: persona que prepara las ventas.

## Datos del pedido

- Cliente existente y activo.
- Una o más líneas, cada una con un producto existente y activo y una cantidad entera mayor que cero.
- El pedido se crea en estado borrador.
- Cada línea conserva el precio unitario del producto vigente cuando se agrega al pedido, expresado como decimal exacto en pesos colombianos.

## Reglas de negocio

- El pedido puede modificarse mientras permanece en borrador.
- No se permite agregar el mismo producto más de una vez; las cantidades se consolidan en una línea.
- Crear o editar el pedido no reserva ni modifica el stock.
- El total se calcula con aritmética decimal exacta; el redondeo se aplica únicamente al precio final de la factura.
- Un pedido borrador puede ser cancelado, pero no se elimina físicamente.

## Historias de usuario

- HU-1: Como empleado, quiero preparar un pedido con productos y cantidades, para revisar una venta antes de facturarla.
- HU-2: Como empleado, quiero ver los precios y el total estimado, para verificar el pedido.
- HU-3: Como empleado, quiero conservar el pedido como borrador, para emitir la factura en un paso posterior.

## Criterios de aceptación

- CA-1: Con cliente y líneas válidas, el sistema crea un pedido en estado borrador y devuelve su identificador y detalle.
- CA-2: El pedido conserva cliente, fecha de creación, productos, cantidades y precios unitarios aplicados.
- CA-3: Si el cliente o un producto no existe o está inactivo, el sistema rechaza la creación sin guardar un pedido parcial.
- CA-4: Si el pedido no tiene líneas, una cantidad no es entera positiva o la solicitud contiene datos inválidos, el sistema informa los errores y no lo crea.
- CA-5: Crear un pedido no cambia el stock ni crea movimientos de inventario.
- CA-6: El total estimado se obtiene usando decimales exactos.
- CA-7: Solo un pedido en borrador puede editarse o cancelarse.

## Casos límite

- Una modificación fallida conserva el borrador anterior completo.
- La existencia de stock al crear el borrador no garantiza su disponibilidad al emitir la factura.
- La desactivación posterior del cliente o de un producto no modifica un pedido borrador ya creado; la emisión debe validar las condiciones aplicables en ese momento.

## Fuera de alcance

- Emitir, anular o imprimir facturas
- Reservar stock
- Aplicar descuentos, impuestos, pagos o crédito
- Enviar el pedido al cliente
