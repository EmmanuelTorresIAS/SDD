# Constitution del proyecto

## Propósito

Sistema para la gestión de inventario, facturación interna mediante PDF y envíos a proveedores. Lo usan principalmente los empleados para gestionar cada movimiento de la mercancía. Resuelve el desorden al gestionar envíos y facturas al cliente por medio de PDF.

### Qué hace
- Registrar los productos disponibles
u +

### Qué no hace (por ahora)
- Generar un dashboard de la actividad mensual
- Emitir factura electrónica con validez ante la DIAN: la factura es un comprobante interno

## Stack tecnológico

| Capa | Tecnología | Motivo |
|------|------------|--------|
| Backend | NestJS con TypeScript | Lo estoy aprendiendo y su estructura por módulos encaja con la arquitectura hexagonal |
| Frontend | React con Vite | Lo estoy aprendiendo y tiene amplia documentación |
| Base de datos | PostgreSQL | Es relacional y transaccional: garantiza que el stock y la factura se actualicen juntos o no se actualicen |
| ORM | TypeORM | Se integra de forma nativa con NestJS |
| Generación de PDF | PDF4.dev | Permite diseñar la factura como plantilla HTML con variables y generarla por REST |
| Pruebas | Pruebas unitarias, de integración y de extremo a extremo con Jest | Viene por defecto en NestJS |

Riesgo aceptado: PDF4.dev es un servicio externo. Si deja de estar disponible, no se pueden generar PDF. Por eso la generación de PDF se accede siempre a través de un puerto, para poder reemplazar el proveedor sin tocar el dominio.

## Arquitectura

Arquitectura hexagonal con DDD, porque es la arquitectura que estoy aprendiendo y permite cambiar la base de datos o el proveedor de PDF sin tocar el dominio.

Estructura: un módulo por área del negocio (inventario, facturación, clientes, envíos). Dentro de cada módulo hay tres capas:

- domain: entidades, value objects y errores del dominio
- application: casos de uso y puertos
- infrastructure: controladores, repositorios y adaptadores (base de datos, PDF)

Regla de dependencias:
- domain no depende de nada
- application depende solo de domain
- infrastructure depende de application y de domain
- los puertos se definen en application y se implementan en infrastructure

## Convenciones de código

- Idioma del código: inglés
- Comentarios: no se escriben comentarios en el código
- Nombres de archivos: kebab-case
- Nombres de clases: PascalCase. Nombres de variables y funciones: camelCase
- Validación: los datos de entrada se validan en el borde con DTOs, y en el dominio con value objects en los atributos que lo ameriten
- Manejo de errores: el dominio lanza errores propios; la capa de infraestructura los traduce a respuestas HTTP
- Mensajes de error: en inglés

## Reglas de calidad

- Pruebas unitarias en todo el código: domain, casos de uso e infrastructure
- Pruebas de integración con la base de datos real
- Pruebas de extremo a extremo solo para los flujos críticos
- Cobertura mínima medida en líneas y ramas: 100% en domain y 95% en el resto
- Se excluyen del cálculo main.ts y los módulos de NestJS
- Definición de terminado: pruebas pasando, cobertura mínima cumplida y ESLint sin errores

## Reglas de negocio

- Moneda: pesos colombianos
- Dinero: se maneja siempre con decimal exacto, nunca con números de punto flotante
- Redondeo: solo en el precio final de la factura
- Stock negativo: prohibido. El descuento de stock y la creación de la factura ocurren en una sola transacción
- Facturas: se pueden editar solo mientras estén en borrador. Una factura emitida no se edita; se anula
- Numeración: las facturas emitidas tienen numeración consecutiva, sin saltos
- Movimientos de inventario: se guarda cada movimiento para tener trazabilidad
- Borrado de datos: prohibido el borrado real. Los datos se marcan como inactivos
- Fechas: se guardan en UTC y se muestran en la zona horaria America/Bogota