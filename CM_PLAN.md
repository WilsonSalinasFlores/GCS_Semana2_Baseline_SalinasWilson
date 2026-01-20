# Plan de Gestión de Configuración (CM_PLAN)
## Proyecto: API de Control de Inventario

## Definición de Elementos de Configuración (EC)

A continuación esta el detalle de los EC que forman parte de la línea base del proyecto. Estos elementos deben estar bajo control de versiones y cualquier cambio debe ser registrado.

| EC | Ubicación | ¿Por qué es EC? | Quién lo modifica |
| :--- | :--- | :--- | :--- |
| **SRS_v1.md** | `/docs/requirements/` | Define el alcance funcional; cualquier cambio altera las pruebas y el diseño. | Analista / PO |
| **SDD.md** | `/docs/design/` | Establece la arquitectura técnica; guía la construcción y asegura la escalabilidad. | Arquitecto / Lead Dev |
| **appsettings.json** | `/src/InventoryAPI/` | Parametriza el sistema (JWT, DB); cambios aquí afectan la ejecución y seguridad. | DevOps / Dev |
| **TestCases.md** | `/docs/tests/` | Valida la calidad del software; permite detectar regresiones en la lógica de stock. | QA / Dev |
| **Código Fuente (.cs)** | `/src/InventoryAPI/` | Implementa la lógica de negocio y controladores; es el producto final entregable. | Desarrollador |
| **Migraciones de BD** | `/src/Data/Migrations/` | Define la evolución del esquema en SQL Server; asegura la integridad de datos. | Dev / DBA / SRE |
| **version-baseline.json**| `/root/` | Controla la trazabilidad y sincronización entre documentos, código y versiones. | Dev Ops / SRE |
| **Inventory.csproj** | `/src/InventoryAPI/` | Gestiona dependencias NuGet y versión del Framework; afecta la compilación. | Arquitecto / Dev |

---

## Justificación del Control
Cada uno de estos elementos ha sido seleccionado porque su modificación no controlada podría generar **deriva de requisitos** (requisitos que cambian sin aviso) o **inconsistencia técnica** (código que no coincide con el diseño). Al mantenerlos como EC en el repositorio, garantizamos que el proyecto sea auditable y recuperable en caso de fallos.
