# Spec 015: Generar PDF de la factura

## Objetivo

Permitir que un empleado genere y descargue un PDF legible de una factura emitida.

## Actores

- Empleado: persona que consulta o entrega el comprobante interno.

## Contenido del PDF

- Número y fecha de emisión de la factura.
- Identificación y nombre o razón social del cliente.
- Código, nombre, talla y color de cada producto, cantidad y precio unitario.
- Subtotales por línea y total final en pesos colombianos.
- Indicación visible de que es un comprobante interno sin validez de factura electrónica ante la DIAN.
- Si la factura está anulada, indicación visible del estado de anulación.

## Reglas de negocio

- Solo se genera el PDF a partir de una factura emitida o anulada.
- El documento se basa en los datos inmutables de la factura, no en los datos actuales del catálogo.
- La generación se realiza mediante el puerto de PDF y el proveedor configurado; el dominio no depende directamente del proveedor externo.
- El PDF no cambia el estado de la factura ni el inventario.

## Historias de usuario

- HU-1: Como empleado, quiero descargar el PDF de una factura, para consultarla o entregarla al cliente.
- HU-2: Como empleado, quiero que el PDF refleje los datos facturados, para conservar el mismo contenido del documento emitido.

## Criterios de aceptación

- CA-1: Para una factura existente emitida, el sistema devuelve un PDF legible con todos los datos requeridos.
- CA-2: Para una factura anulada, el PDF informa claramente que está anulada.
- CA-3: Si la factura no existe o sigue en borrador, el sistema no genera PDF y explica el motivo.
- CA-4: Si el proveedor PDF no está disponible o responde con error, el sistema informa que no pudo generarse el documento; la factura permanece intacta.
- CA-5: Los valores, número y datos de producto del PDF coinciden con la factura almacenada.
- CA-6: La descarga usa un tipo de contenido PDF y un nombre de archivo que identifica la factura sin caracteres inválidos.

## Casos límite

- Volver a solicitar el PDF no emite una nueva factura ni altera su numeración.
- El PDF de una factura histórica conserva sus datos aun si posteriormente cambian o se desactivan el cliente o los productos.
- Un error externo de generación no se presenta como descarga exitosa.

## Fuera de alcance

- Factura electrónica ante la DIAN
- Envío automático por correo o almacenamiento permanente del archivo
- Personalización de plantillas desde la interfaz
- Edición del contenido de una factura emitida
