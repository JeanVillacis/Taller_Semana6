# Historias Técnicas

## HT-001 – Configuración del Proyecto Base
`Story Points: 2`

**Justificación SP:** Infraestructura base sin lógica de negocio, pero es la base del proyecto y requiere configuración de entorno.


### DEV
| # | Tarea |
|---|-------|
| 1 | Inicializar proyecto Spring Boot con dependencias: Web, Data JPA, Validation, Security y JWT|
| 2 | Configurar `application.properties` con las variables de entorno para la conexión a la BD |
| 3 | Crear `Dockerfile` para la aplicación Spring Boot |
| 4 | Crear `docker-compose.yml` que levante la aplicación Spring Boot |
| 5 | Implementar endpoint `GET /api/health` |

### QA
| # | Tarea |
|---|-------|
| --- | --- |

---

## HT-002 – Diseño de la Base de Datos
`Story Points: 3`

**Justificación SP:** Define el esquema completo del sistema con relaciones entre múltiples entidades y constraints de integridad referencial.

### DEV
| # | Tarea |
|---|-------|
| 1 | Definir entidades JPA: `Asegurado`, `Vehiculo`, `Poliza`, `Reclamo`, `ReclamoFotografia`, `ReclamoBandera` |
| 2 | Configurar relaciones `@OneToMany` y `@ManyToOne` entre entidades |
| 3 | Agregar contenedor PostgreSQL al `docker-compose.yml` con variables de entorno |
| 4 | Configurar `spring.jpa.hibernate.ddl-auto` en `application.properties` para la generación automática de tablas |
| 5 | Agregar constraint de integridad referencial: no eliminar asegurado con pólizas vinculadas |

### QA
| # | Tarea |
|---|-------|
| --- | --- |

---

## HT-003 – Seguridad y Control de Acceso
`Story Points: 5`

**Justificación SP:** Involucra Spring Security, JWT, filtros de autenticación y control de acceso por roles.

### DEV
| # | Tarea |
|---|-------|
| 1 | Crear entidad `Usuario` con atributos (email, password, rol)|
| 2 | Implementar repositorio `UsuarioRepository` |
| 3 | Implementar `POST /api/v1/auth/login` que valida credenciales y retorna token JWT |
| 4 | Implementar filtro JWT para validar token en cada request protegido |
| 5 | Configurar `SecurityFilterChain` con reglas por rol: GESTOR, ASEGURADO |
| 6 | Hashear contraseñas antes de guardarlas |

### QA
| # | Tarea |
|---|-------|
| --- | --- |

---

# Historias de Usuario

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