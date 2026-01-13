# Casos de Prueba (Test Plan)
**Proyecto:** API de Control de Inventario  
**Referencia de Diseño:** SDD.md v1.1  
**Referencia de Requisitos:** SRS.md v1.2

## 1. Introducción
Este documento detalla los casos de prueba necesarios para validar la integridad de la API de Inventario. Las pruebas se centran en la lógica de negocio (Capa de Servicios) y la seguridad de los endpoints.

## 2. Ambiente de Pruebas
- **Herramienta:** Postman / Swagger UI.
- **Base de Datos:** SQL Server (Instancia de Desarrollo).
- **Servidor:** Localhost (Kestrel / IIS Express).

## 3. Casos de Prueba Funcionales (RF)

| ID | Requisito Relacionado | Descripción | Pasos de Prueba | Resultado Esperado |
| :--- | :--- | :--- | :--- | :--- |
| **CP-01** | RF-01 (CRUD) | Creación exitosa de producto | Enviar POST a `/api/productos` con JSON válido. | Status 201 Created y objeto con ID asignado. |
| **CP-02** | RF-02 (Categorías) | Validación de categoría inexistente | Enviar POST a `/api/productos` con un `CategoriaId` que no existe. | Status 400 Bad Request o 404 Not Found. |
| **CP-03** | RF-03 (Stock) | Registro de entrada de stock | Enviar POST a `/api/movimientos` sumando 10 unidades a un producto. | El campo `CantidadActual` en la tabla productos aumenta en 10. |
| **CP-04** | RF-03 (Stock) | Validación de stock insuficiente | Intentar registrar una salida (venta) mayor al stock actual. | Status 400 Bad Request con mensaje "Stock insuficiente". |

## 4. Casos de Prueba No Funcionales (RNF)

| ID | Requisito Relacionado | Descripción | Pasos de Prueba | Resultado Esperado |
| :--- | :--- | :--- | :--- | :--- |
| **CP-05** | RNF-01 (Seguridad) | Acceso denegado sin Token | Intentar un GET a `/api/productos` sin encabezado Authorization. | Status 401 Unauthorized. |
| **CP-06** | RNF-01 (Seguridad) | Acceso concedido con JWT | Enviar petición con Bearer Token válido obtenido del login. | Status 200 OK y lista de datos. |
| **CP-07** | RNF-02 (Rendimiento) | Tiempo de respuesta en búsquedas | Realizar un GET masivo de productos. | El tiempo de respuesta (TTFB) debe ser < 200ms. |

## 5. Matriz de Trazabilidad
Este proyecto asegura que:
1. Todo **Requisito (SRS)** tiene un **Componente (SDD)**.
2. Todo **Componente (SDD)** tiene una **Configuración (appsettings.json)**.
3. Toda **Configuración** es validada por un **Caso de Prueba (CP)**.

---
**Estado Final de la Prueba:** [ ] Pendiente | [X] Pass | [ ] Fail
**Revisado por:** Wilson Salinas