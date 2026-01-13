# Software Requirements Specification (SRS) 
## Proyecto: API de Control de Inventario

**Autor:** Wilson Salinas 
**Fecha:** 12 de enero de 2026  
**Tecnologías:** .NET / Entity Framework Core / SQL Server

---

## 1. Introducción
Este documento define los requisitos para una Web API encargada de la gestión de inventarios. El sistema servirá como el núcleo de datos para controlar productos, categorías, proveedores y movimientos de stock, permitiendo una integración fluida con clientes web o móviles.

## 2. Requisitos Funcionales (RF)

| ID | Requisito | Descripción |
| :--- | :--- | :--- |
| **RF-01** | **Gestión de Catálogo (CRUD)** | El sistema debe permitir el mantenimiento completo de productos: creación, lectura, actualización y eliminación (borrado lógico). |
| **RF-02** | **Organización por Categorías** | Los productos deben estar asociados a categorías para permitir la segmentación y filtrado eficiente de la información. |
| **RF-03** | **Control de Stock y Movimientos** | El sistema debe registrar entradas (compras) y salidas (ventas/ajustes), actualizando el balance de stock en tiempo real en la tabla de productos. |
| **RF-04** | **Vinculación con Proveedores** | El sistema debe permitir asociar cada producto a uno o varios proveedores, manteniendo datos de contacto y RUC/NIT. |

## 3. Requisitos No Funcionales (RNF)

| ID | Requisito | Descripción |
| :--- | :--- | :--- |
| **RNF-01** | **Autenticación y Seguridad** | El acceso a los controladores de la API debe estar restringido mediante **JWT (JSON Web Tokens)** y políticas de CORS. |
| **RNF-02** | **Integridad de Datos** | Se deben implementar transacciones de base de datos para asegurar que, si un registro de movimiento de stock falla, el balance del producto no se altere. |

## 4. Modelado de Datos (Diagrama de Entidad-Relación)

A continuación, se presenta la estructura sugerida para las tablas que se generarán mediante **Entity Framework Core (Code First)**.



---

## 5. Diseño Técnico
- **Arquitectura:** MVC (Model-View-Controller) / Web API.
- **ORM:** Entity Framework Core.
- **Base de Datos:** SQL Server.
- **Validaciones:** Uso de `DataAnnotation` en los modelos para asegurar la calidad de los datos de entrada.