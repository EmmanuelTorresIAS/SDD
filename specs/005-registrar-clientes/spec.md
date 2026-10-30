# Spec 005: Registrar clientes

## Objetivo

Permitir que un empleado registre clientes con sus datos de identificación y contacto para asociarlos a pedidos y facturas.

## Actores

- Empleado: persona que administra clientes y ventas.

## Datos del cliente

| Dato | Obligatorio | Regla |
|---|---|---|
| Tipo de identificación | Sí | Tipo admitido por el negocio |
| Número de identificación | Sí | Entre 3 y 30 caracteres; sin espacios al inicio ni al final |
| Nombre o razón social | Sí | Entre 3 y 150 caracteres |
| Teléfono | No | Hasta 30 caracteres |
| Correo electrónico | No | Formato de correo válido; hasta 254 caracteres |

La combinación de tipo y número de identificación es única en todo el sistema. La identificación se compara sin distinguir mayúsculas y minúsculas.

## Historias de usuario

- HU-1: Como empleado, quiero registrar un cliente con identificación y contacto, para asociarlo a sus pedidos.
- HU-2: Como empleado, quiero que el sistema rechace identificaciones repetidas, para evitar clientes duplicados.
- HU-3: Como empleado, quiero conocer todos los errores de validación, para corregir los datos en un solo intento.

## Criterios de aceptación

- CA-1: Con los datos obligatorios válidos, el sistema crea el cliente activo e informa el resultado.
- CA-2: El sistema registra la fecha y hora de creación en UTC.
- CA-3: El tipo y número de identificación ya registrados, incluso para un cliente inactivo, no se pueden volver a registrar.
- CA-4: Si falta un dato obligatorio o solo contiene espacios, el sistema rechaza el registro e identifica el campo.
- CA-5: Si el correo tiene formato inválido o un campo supera su longitud máxima, el sistema rechaza la solicitud e identifica todos los errores.
- CA-6: Si ocurre un error, no queda un cliente creado parcialmente.

## Casos límite

- Se eliminan espacios al inicio y al final antes de validar y guardar.
- Los campos opcionales pueden omitirse o quedar vacíos.
- Dos solicitudes simultáneas con la misma identificación solo pueden crear un cliente; la otra se rechaza como duplicada.

## Fuera de alcance

- Consultar, editar o desactivar clientes
- Importar clientes de forma masiva
- Verificar identidad con servicios externos
- Registrar direcciones de envío o datos de pago
