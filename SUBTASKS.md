## HT-001 – Configuración del Proyecto Base
`Story Points: 2`

**Justificación SP:** Infraestructura base sin lógica de negocio, pero es la base del proyecto y requiere configuración de entorno.


### DEV
| # | Tarea |
|---|-------|
| 1 | Inicializar proyecto Spring Boot con dependencias: Web, Data JPA, Validation, Security |
| 2 | Configurar `application.properties` con las variables de entorno para la conexión a la BD |
| 3 | Crear `Dockerfile` para la aplicación Spring Boot |
| 4 | Crear `docker-compose.yml` que levante la aplicación Spring Boot y la BD |
| 5 | Implementar endpoint `GET /api/health` |

### QA
| # | Tarea |
|---|-------|
| --- | --- |

---

## HU-001 – Registro de Asegurado
`Story Points: 3`

**Justificación SP:** Validaciones múltiples y manejo de varios escenarios de error.

### DEV
| # | Tarea |
|---|-------|
| 1 | Crear entidad JPA `Asegurado` con sus atributos (nombre, apellido, numeroIdentificacion, direccion, telefono, correoElectronico) |
| 2 | Implementar repositorio `AseguradoRepository` |
| 3 | Implementar validaciones de unicidad de identificacion y correo |
| 4 | Crear DTO `AseguradoDTO` |
| 5 | Crear service `AseguradoService` con la logica de negocio para registrar asegurados |
| 6 | Implementar `POST /api/v1/asegurados` en el controller |

### QA
| # | Tarea |
|---|-------|
| --- | --- |