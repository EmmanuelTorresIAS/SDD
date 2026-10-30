# Spec 013: Emitir factura

## Objetivo

Convertir un pedido válido en una factura interna emitida, asignarle numeración consecutiva y descontar el stock de forma atómica.

## Actores

- Empleado: persona autorizada para facturar.

## Reglas de negocio

- Solo se emite una factura desde un pedido en estado borrador y todavía no facturado.
- El cliente y los productos deben existir y estar activos al emitir.
- Cada producto debe tener stock suficiente para cubrir la cantidad pedida.
- El precio unitario aplicado se toma del pedido; la factura conserva una copia inmutable de los datos y precios facturados.
- La numeración de facturas emitidas es consecutiva y no presenta saltos.
- La creación de la factura, asignación del número, cambio de estado del pedido, descuento de todo el stock y creación de movimientos de salida ocurren en una sola transacción.
- Los valores monetarios usan decimales exactos en pesos colombianos; el redondeo se aplica solo al precio final de la factura.
- La factura es un comprobante interno y no tiene validez de factura electrónica ante la DIAN.

## Historias de usuario

- HU-1: Como empleado, quiero emitir la factura de un pedido, para confirmar la venta.
- HU-2: Como empleado, quiero que el sistema descuente el inventario junto con la factura, para evitar diferencias.
- HU-3: Como empleado, quiero una numeración consecutiva, para identificar las facturas emitidas.

## Criterios de aceptación

- CA-1: Dado un borrador válido con stock suficiente, el sistema emite una factura con número consecutivo y confirma el resultado.
- CA-2: La factura contiene el cliente, las líneas, cantidades, precios unitarios, totales y fecha de emisión.
- CA-3: La emisión reduce el stock de cada producto y crea un movimiento de salida asociado a la factura.
- CA-4: Si algún producto no tiene stock suficiente, el sistema rechaza la emisión completa; no hay factura, número consumido, cambio de estado, descuento ni movimientos parciales.
- CA-5: Si ocurre cualquier error al emitir, todos los cambios de la operación se revierten.
- CA-6: Si se solicita emitir un pedido ya facturado, cancelado o que no existe, el sistema rechaza la solicitud sin crear otra factura.
- CA-7: Solicitudes concurrentes no pueden emitir dos veces el mismo pedido ni asignar números duplicados.
- CA-8: La factura emitida no puede editarse; cualquier corrección posterior requiere anulación.

## Casos límite

- El stock se vuelve a validar al emitir, aunque haya sido suficiente al crear el pedido.
- Si dos pedidos concurrentes compiten por las últimas unidades, como máximo se emiten los que puedan mantener stock no negativo.
- La reserva de numeración debe ser compatible con la regla de no tener saltos aun ante fallos y concurrencia.

## Fuera de alcance

- Facturación electrónica con validez DIAN
- Pagos, impuestos, descuentos, devoluciones parciales o crédito
- Generar o almacenar el PDF
- Editar facturas emitidas
