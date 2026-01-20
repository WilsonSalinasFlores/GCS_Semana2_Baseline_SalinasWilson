# Ciclo de Desarrollo

## Immpacto por fases

*"El RNF de búsqueda de productos debe ser $\leq$ 2 segundos"*. El objetivo es demostrar que el cambio sin un control estricto de la configuración incrementa los costos y genera deudas técnicas.

| Fase | ¿Qué cambia? | EC afectados | Riesgo si no se controla | Evidencia de validación |
| :--- | :--- | :--- | :--- | :--- |
| **Requisitos** | Actualizar el RNF de rendimiento y los criterios de aceptación técnicos. | `SRS_v1.md` | **Ambigüedad:** El equipo desarrolla sin una meta clara, lo que causa un retrabajo costoso. | Checklist y acta de revisión formal de requisitos. |
| **Diseño** | Ajustar la arquitectura de consultas o definir una estrategia de caché de datos. | `SDD.md` | **Arquitectura ineficiente:** Se generan cuellos de botella que impiden el escalamiento del sistema. | Diagrama de arquitectura o flujo actualizado. |
| **Codificación** | Optimizar consultas LINQ e implementar índices en las tablas de la base de datos. | Código Fuente (`/src`) | **"Funciona en mi PC":** El código no está optimizado y falla bajo condiciones de carga real. | Captura de commit con descripción técnica del cambio. |
| **Pruebas** | Diseñar scripts de medición de latencia y pruebas de carga concurrentes. | Casos de Prueba (`/tests`) | **Fuga de errores:** Se entrega un producto que no cumple con el nivel de servicio prometido. | Captura de ejecución de pruebas (ej. JMeter o Postman). |

