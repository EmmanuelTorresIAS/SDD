# Spec 002: Consultar productos

## Objetivo

Permitir que un empleado consulte productos activos, busque por código o nombre y vea el detalle de un producto.

## Actores

- Empleado: persona que gestiona el catálogo y la mercancía.

## Reglas de consulta

- El listado muestra productos activos por defecto y permite paginar los resultados.
- Los resultados se ordenan por código de forma ascendente.
- La búsqueda admite coincidencias parciales en código o nombre, sin distinguir mayúsculas de minúsculas.
- Si se informa un término, se muestran los productos que coincidan en el código o en el nombre.
- La consulta detallada identifica un producto por su código único.
- El detalle incluye código, nombre, categoría, precio de venta, talla, color, estado y fecha de creación.
- Los productos inactivos no aparecen en el listado por defecto; una consulta detallada puede encontrarlos e indica claramente que están inactivos.
- Esta funcionalidad no modifica productos ni su stock.

## Historias de usuario

- HU-1: Como empleado, quiero listar productos activos, para conocer el catálogo disponible.
- HU-2: Como empleado, quiero buscar productos por código o nombre, para encontrar uno sin recorrer todo el catálogo.
- HU-3: Como empleado, quiero ver el detalle de un producto, para consultar todos sus datos.

## Criterios de aceptación

### Listado y búsqueda

- CA-1: Cuando el empleado consulta el listado sin filtros, el sistema devuelve los productos activos ordenados por código.
- CA-2: Cuando el empleado busca un término, el sistema devuelve los productos cuyo código o nombre contiene ese término, sin distinguir mayúsculas de minúsculas.
- CA-3: Cuando no hay coincidencias, el sistema devuelve un listado vacío y no un error.
- CA-4: El listado permite navegar resultados paginados sin repetir ni omitir registros entre páginas mientras los datos no cambien.
- CA-5: Un producto inactivo no aparece en el listado normal.

### Detalle

- CA-6: Cuando el empleado consulta un código existente, el sistema muestra todos los datos definidos para el detalle.
- CA-7: Si el código no existe, el sistema informa que el producto no fue encontrado.
- CA-8: Si el código pertenece a un producto inactivo, el detalle lo informa explícitamente.

## Casos límite

- Una búsqueda vacía o compuesta solo por espacios se trata como consulta sin término.
- Los códigos se buscan sin distinguir mayúsculas de minúsculas.
- Los valores opcionales de talla y color se muestran vacíos cuando no fueron registrados.
- Los errores de consulta no alteran el catálogo.

## Fuera de alcance

- Crear, editar o desactivar productos
- Consultar stock o movimientos de inventario
- Filtrar por categoría, talla, color o precio
- Exportar el catálogo o descargar imágenes
