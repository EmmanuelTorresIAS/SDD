# Spec 016: Registrar proveedores

## Objetivo

Permitir que un empleado registre proveedores con datos básicos de identificación y contacto para asociarlos a envíos.

## Actores

- Empleado: persona que coordina recepción y envíos de mercancía.

## Datos del proveedor

| Dato | Obligatorio | Regla |
|---|---|---|
| Nombre o razón social | Sí | Entre 3 y 150 caracteres |
| Identificación | No | Hasta 30 caracteres |
| Teléfono | No | Hasta 30 caracteres |
| Correo electrónico | No | Formato válido; hasta 254 caracteres |
| Dirección | No | Hasta 250 caracteres |

Si se proporciona identificación, esta es única en el sistema. El nombre o razón social, con espacios exteriores eliminados, es obligatorio.

## Historias de usuario

- HU-1: Como empleado, quiero registrar un proveedor y sus datos de contacto, para asociarlo a los envíos.
- HU-2: Como empleado, quiero que se rechacen datos inválidos o identificaciones duplicadas, para evitar registros inconsistentes.

## Criterios de aceptación

- CA-1: Con nombre válido y los demás datos opcionales válidos, el sistema crea un proveedor activo y confirma el resultado.
- CA-2: El sistema registra la fecha y hora de creación en UTC.
- CA-3: Si se informa una identificación ya utilizada, el sistema rechaza el registro.
- CA-4: Si falta el nombre, el correo no tiene formato válido o algún valor supera su límite, el sistema informa todos los errores y no crea el proveedor.
- CA-5: Un error no deja un proveedor parcialmente guardado.

## Casos límite

- Los espacios exteriores se eliminan antes de validar y guardar.
- Un dato opcional omitido se conserva vacío, no como un texto de espacios.
- Dos registros concurrentes con la misma identificación no pueden crear proveedores duplicados.

## Fuera de alcance

- Editar, consultar o desactivar proveedores
- Gestionar pagos, contratos o calificaciones
- Importación masiva de proveedores
