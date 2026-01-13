# Software Design Document (SDD)
## Proyecto: API de Control de Inventario

**Arquitectura:** Layered Architecture (Arquitectura en Capas)  
**Entorno:** .NET Web API / SQL Server

---

## 1. Introducción
Este documento describe el diseño técnico y las decisiones de arquitectura para la API de Inventario. Se busca una estructura desacoplada que permita el mantenimiento y la escalabilidad del sistema, separando la lógica de persistencia de la lógica de negocio.

## 2. Arquitectura del Sistema
Se ha seleccionado una **Arquitectura en Capas** para organizar los componentes del proyecto. Esta decisión facilita las pruebas unitarias y el intercambio de proveedores de datos si fuera necesario.



### Descripción de las Capas:
* **Capa de Presentación (Controllers):** Define los endpoints REST. Se encarga de recibir objetos DTO, validar el estado del modelo y devolver códigos de estado HTTP (200, 201, 400, 404).
* **Capa de Negocio (Services/Logic):** Contiene las reglas de validación (ej. no permitir salidas de stock si el balance es insuficiente) y procesa los datos antes de guardarlos.
* **Capa de Acceso a Datos (Data/Models):** Utiliza **Entity Framework Core** para interactuar con SQL Server. Aquí reside el `DbContext` y las configuraciones de las entidades.

## 3. Diseño de Componentes Lógicos

| Componente | Responsabilidad |
| :--- | :--- |
| **Auth Middleware** | Valida la autenticidad de las peticiones mediante tokens **JWT**. |
| **Inventory Controller** | Orquestador de las peticiones CRUD de productos y categorías. |
| **Movement Engine** | Lógica especializada para el cálculo de stock (Entradas/Salidas) garantizando la atomicidad de las transacciones. |
| **Persistence Context** | Mapeo de objetos POCO a tablas relacionales mediante **Fluent API**. |

## 4. Diseño de la Base de Datos
El sistema utiliza una base de datos relacional normalizada. Las relaciones se gestionarán mediante claves foráneas para asegurar la integridad referencial.



### Entidades Principales:
* **Productos:** Almacena la información maestra y el saldo actual de stock.
* **Categorias:** Clasificación jerárquica de productos.
* **MovimientosDeInventario:** Histórico detallado de cada cambio en el inventario (Tipo: Entrada/Salida).
* **Proveedores:** Datos de los proveedores asociados a los productos.

## 5. Decisiones Técnicas

1.  **Framework:** .NET 8/9 por su alto rendimiento y soporte nativo para contenedores.
2.  **ORM:** Entity Framework Core (Enfoque **Code First**) para mantener el versionamiento de la base de datos mediante migraciones.
3.  **Seguridad:** Implementación de **JWT** para el manejo de sesiones Stateless, ideal para APIs.
4.  **Transferencia de Datos:** Uso de **DTOs (Data Transfer Objects)** para evitar el acoplamiento directo entre la base de datos y la vista (JSON), previniendo problemas de sobre-exposición de datos.
5.  **Validación de Datos:** Uso de `DataAnnotations` en los modelos y lógica personalizada en la capa de servicios para asegurar que el stock nunca sea negativo.

---

## 6. Diagrama de Flujo (Ejemplo: Salida de Stock)
1. El cliente envía un `StockRequestDTO`.
2. El controlador valida el token JWT.
3. El servicio verifica si existe stock suficiente.
4. Si es válido, se crea el registro en `MovimientosDeInventario` y se actualiza el campo `Stock` en `Productos` dentro de una transacción.
5. Se retorna un código `201 Created`.