# Spec 018: Consultar y actualizar envíos

## Objetivo

Permitir que un empleado consulte envíos registrados y actualice su estado para dar seguimiento a la mercancía esperada.

## Actores

- Empleado: persona que coordina y supervisa envíos.

## Estados

- Pendiente: registrado y aún no despachado.
- En tránsito: despachado por el proveedor.
- Recibido: la mercancía llegó.
- Cancelado: el envío fue cancelado antes de completarse.

Transiciones permitidas: pendiente a en tránsito o cancelado; en tránsito a recibido o cancelado. Los estados recibido y cancelado son terminales.

## Reglas de negocio

- El listado se pagina y ordena por fecha de creación descendente.
- El detalle muestra proveedor, referencia, estado, fechas disponibles y líneas de producto con cantidades.
- Cada cambio de estado registra fecha UTC y empleado cuando su identidad esté disponible.
- Actualizar el estado no cambia stock; el ingreso físico se registra mediante la entrada de inventario.
- Un estado terminal no se puede cambiar.

## Historias de usuario

- HU-1: Como empleado, quiero consultar los envíos y sus estados, para conocer la mercancía pendiente o en camino.
- HU-2: Como empleado, quiero actualizar el estado de un envío, para reflejar su progreso.
- HU-3: Como empleado, quiero que se rechacen transiciones inválidas, para conservar un seguimiento coherente.

## Criterios de aceptación

- CA-1: El listado devuelve envíos paginados en orden descendente de creación y permite filtrar por estado.
- CA-2: El detalle de un envío existente muestra todos los datos y líneas registrados.
- CA-3: Una transición permitida actualiza el estado y registra cuándo ocurrió.
- CA-4: Una transición no permitida, un estado desconocido o un envío inexistente se rechazan sin alterar el envío.
- CA-5: Un envío recibido o cancelado no admite más cambios de estado.
- CA-6: Consultar o actualizar el envío no modifica el stock ni crea movimientos.

## Casos límite

- Dos actualizaciones concurrentes no deben permitir una transición que sería inválida desde el estado más reciente.
- Los envíos siguen siendo consultables aunque el proveedor o un producto asociado esté inactivo.
- El filtro de estado no altera el orden ni la paginación de los resultados.

## Fuera de alcance

- Registrar o corregir entradas de inventario
- Crear o editar envíos
- Gestionar seguimiento de transportistas externos
- Notificaciones automáticas al proveedor
