# Spec 001: Registrar productos

## Objetivo

Permitir que un empleado registre un producto nuevo en el sistema con sus datos básicos, para poder controlarlo después en el inventario y facturarlo.

## Actores

- Empleado: persona que gestiona la mercancía del negocio.

## Datos del producto

| Dato | Obligatorio | Regla |
|---|---|---|
| Código | Sí | Único en todo el sistema. Entre 3 y 30 caracteres, sin espacios al inicio ni al final |
| Nombre | Sí | Entre 3 y 100 caracteres, sin espacios al inicio ni al final |
| Categoría | Sí | Texto entre 3 y 50 caracteres |
| Precio de venta | Sí | Mayor que cero, en pesos colombianos |
| Talla | No | Texto de hasta 10 caracteres |
| Color | No | Texto de hasta 30 caracteres |

Cada combinación de talla y color de una prenda se registra como un producto independiente, con su propio código.

## Historias de usuario

- HU-1: Como empleado, quiero registrar un producto con sus datos básicos, para poder controlarlo en el inventario.
- HU-2: Como empleado, quiero que el sistema rechace códigos repetidos, para no tener dos productos que se confundan entre sí.
- HU-3: Como empleado, quiero que el sistema me indique qué datos son incorrectos, para poder corregirlos sin adivinar.

## Criterios de aceptación

### Registro correcto

- CA-1: Dado un producto con todos los datos obligatorios válidos, cuando el empleado lo registra, entonces el producto queda guardado y se le informa que el registro fue exitoso.
- CA-2: Dado un producto registrado correctamente, entonces queda activo y con stock cero.
- CA-3: Dado un producto sin talla ni color, cuando el empleado lo registra con los demás datos válidos, entonces el registro es exitoso.
- CA-4: Dado un producto registrado correctamente, entonces el sistema guarda la fecha y hora de su creación.

### Código único

- CA-5: Dado un código que ya pertenece a un producto registrado, cuando el empleado intenta registrar otro producto con ese código, entonces el sistema lo rechaza y no guarda nada.
- CA-6: Dado un código que ya existe escrito en mayúsculas, cuando el empleado intenta registrar el mismo código en minúsculas, entonces el sistema lo rechaza.
- CA-7: Dado un código que pertenece a un producto inactivo, cuando el empleado intenta registrar otro producto con ese código, entonces el sistema lo rechaza.

### Datos obligatorios

- CA-8: Dado un producto al que le falta el código, el nombre, la categoría o el precio, cuando el empleado intenta registrarlo, entonces el sistema lo rechaza e indica qué dato falta.
- CA-9: Dado un dato obligatorio compuesto solo por espacios, cuando el empleado intenta registrarlo, entonces el sistema lo trata como vacío y lo rechaza.

### Datos inválidos

- CA-10: Dado un precio igual a cero o negativo, cuando el empleado intenta registrar el producto, entonces el sistema lo rechaza e indica que el precio debe ser mayor que cero.
- CA-11: Dado un precio que no es un número, cuando el empleado intenta registrar el producto, entonces el sistema lo rechaza.
- CA-12: Dado un código, nombre, categoría, talla o color que supera su longitud máxima o no alcanza la mínima, cuando el empleado intenta registrar el producto, entonces el sistema lo rechaza e indica qué dato incumple la regla.
- CA-13: Dado un producto con varios datos inválidos, cuando el empleado intenta registrarlo, entonces el sistema informa todos los errores a la vez.

## Casos límite

- Espacios al inicio o al final: el sistema los elimina antes de validar y de guardar.
- Código con mayúsculas y minúsculas: se compara sin distinguirlas y se guarda en mayúsculas.
- Dos empleados registran el mismo código al mismo tiempo: solo uno de los registros se guarda y el otro es rechazado como código repetido.
- Un registro rechazado no deja ningún dato guardado, ni parcial.

## Fuera de alcance

- Editar un producto ya registrado
- Desactivar un producto
- Consultar o listar productos
- Registrar stock inicial: el stock entra por movimientos de inventario, en otra funcionalidad
- Imágenes del producto
- Productos con variantes agrupadas bajo un mismo producto
- Carga masiva de productos