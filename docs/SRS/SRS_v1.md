# Software Requirements Specification (SRS) 
## Proyecto: API de Control de Inventario

**Autor:** Wilson Salinas 
**Fecha:** 12 de enero de 2026  
**Tecnologías:** .NET / Entity Framework Core / SQL Server

**Estado:** Línea Base Controlada  
**Última Actualización:** 13 de enero de 2026
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
| **RNF-05** | **Autenticación y Seguridad** | El acceso a los controladores de la API debe estar restringido mediante **JWT (JSON Web Tokens)** y políticas de CORS. |
| **RNF-06** | **Integridad de Datos** | Se deben implementar transacciones de base de datos para asegurar que, si un registro de movimiento de stock falla, el balance del producto no se altere. |
| **RNF-07**| **Bitácora de Auditoría (Audit Log)** | **El sistema debe registrar automáticamente quién, cuándo y qué cambio se realizó en los datos maestros de productos y niveles de stock para asegurar la trazabilidad.** |


## 4. Trazabilidad de Requisitos
El nuevo requisito **RNF-07** es fundamental para el cumplimiento de normativas de control interno, asegurando que cada ajuste manual al inventario tenga un responsable identificado en la base de datos.