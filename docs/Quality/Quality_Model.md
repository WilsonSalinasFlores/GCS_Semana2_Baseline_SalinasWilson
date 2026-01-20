# Modelo de Calidad del Software
**Estándar:** ISO/IEC 25010

| Atributo | Definición (1 línea) | Métrica verificable | EC que lo soporta |
| :--- | :--- | :--- | :--- |
| **Mantenibilidad** | Facilidad para modificar el software sin introducir errores. | Índice de mantenibilidad $\geq 70/100$ en Visual Studio. | `/src` |
| **Seguridad** | Protección de datos contra accesos no autorizados. | 0 contraseñas en texto plano; uso obligatorio de JWT. | `/appsettings.json` |
| **Adecuación Funcional** | Grado en que las funciones cumplen los requisitos del negocio. | 100% de los requisitos del SRS aprobados en TestCases. | `SRS_v1.md`, `TestCases.md` |
| **Eficiencia** | Comportamiento relativo a los tiempos de respuesta del sistema. | Latencia $\leq 300ms$ en el 95% de las consultas GET. | `/src` (Controladores) |
| **Fiabilidad** | Capacidad de mantener su nivel de prestación bajo condiciones dadas. | Tasa de éxito de peticiones $\geq 99.9\%$ en pruebas de carga. | `/src`, `TestCases.md` |
| **Compatibilidad** | Capacidad de la API para intercambiar datos con otros sistemas. | Validación exitosa contra el esquema OpenAPI 3.0 (Swagger). | `SDD.md`, `/src` |

### Métricas "Estrella" del Proyecto
1. **Adecuación Funcional:** Garantiza que el inventario sea exacto según las reglas del negocio definidas en el SRS.
2. **Eficiencia:** Asegura que la arquitectura diseñada en el SDD soporte la carga de usuarios concurrentes sin degradar la experiencia.