# Spec 017: Registrar envíos

## Objetivo

Permitir que un empleado registre un envío asociado a un proveedor y detalle los productos y cantidades esperados.

## Actores

- Empleado: persona que coordina la recepción de mercancía.

## Datos del envío

- Proveedor existente y activo.
- Una o más líneas con producto existente, cantidad entera mayor que cero y, opcionalmente, referencia del proveedor.
- Fecha de registro UTC y estado inicial pendiente.
- Una referencia externa del envío puede registrarse opcionalmente para facilitar su seguimiento.

## Reglas de negocio

- El envío es un registro de seguimiento y no incrementa stock al crearse ni al cambiar su estado.
- Las entradas físicas de mercancía se registran mediante la funcionalidad de entrada de inventario.
- El envío conserva la descripción y cantidades registradas; los productos no se pueden borrar físicamente.
- No se permite registrar un envío sin líneas.

## Historias de usuario

- HU-1: Como empleado, quiero registrar un envío de un proveedor, para dar seguimiento a mercancía esperada.
- HU-2: Como empleado, quiero detallar productos y cantidades, para comparar lo esperado con lo recibido.

## Criterios de aceptación

- CA-1: Con proveedor y líneas válidos, el sistema crea el envío en estado pendiente y confirma el resultado.
- CA-2: El envío conserva proveedor, productos, cantidades, referencia y fecha de creación.
- CA-3: Si el proveedor no existe o está inactivo, el sistema rechaza el registro.
- CA-4: Si algún producto no existe, la cantidad no es entera positiva o no hay líneas, el sistema informa los errores y no guarda el envío parcialmente.
- CA-5: Registrar el envío no altera stock ni crea movimientos de inventario.
- CA-6: El envío se conserva aunque el proveedor o un producto se desactive después de su creación.

## Casos límite

- Una misma referencia externa puede omitirse; si se proporciona, no se asume que sea globalmente única salvo que el negocio lo establezca.
- El registro repetido de una misma solicitud crea otro envío si no se proporciona un identificador de idempotencia.
- Una modificación posterior de los datos del proveedor no cambia la referencia histórica del envío.

## Fuera de alcance

- Actualizar el estado del envío
- Aumentar stock automáticamente
- Gestionar transportistas, costos, pagos o devoluciones
- Consultar y exportar listados de envíos
