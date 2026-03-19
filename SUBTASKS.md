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
**Justificación SP:** En el rol de QA para esta historia de usuario refleja la necesidad de validar  las reglas de negocio y casos límite para asegurar la integridad de los datos.
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1| Diseñar la matriz de datos de prueba con diferentes combinaciones de datos válidos e inválidos: campos vacíos, identificaciones duplicadas, correos con formato incorrecto, y casos límite en longitudes de campos | Medio |
| 2| Escribir tests unitarios del servicio de negocio para verificar que las validaciones de unicidad y formato| Medio |
|3 | Crear tests de integración para el endpoint POST para probar el flujo completo desde el controller, validando respuestas HTTP y estructura de errores | Alto |
|4 | Ejecutar pruebas exploratorias sobre el registro utilizando pruebas automatizadas| Medio |
| 5 | Documentar hallazgos y casos de prueba ejecutados, registrando resultados obtenidos | Bajo |
## HU-002 – Consultar Asegurados
`Story Points: 2`
 
**Justificación SP:** Solo lectura con dos endpoints simples y manejo de un único caso de error.
 
### DEV
| # | Tarea |
|---|-------|
| 1 | Implementar `GET /api/v1/asegurados` que retorna lista con información básica de cada asegurado |
| 2 | Implementar `GET /api/v1/asegurados/{id}` que retorna el detalle completo del asegurado |
| 3 | Manejar excepción cuando el asegurado no existe |
 
### QA
**Justificación SP:** En el rol de QA se concentra en verificar diferentes escenarios de consulta, casos límite y performance básica.

| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Generar datos de prueba en la base de datos para validar que el listado y la consulta individual funcionen  | Bajo |
| 2 | Escribir tests de integración para ambos endpoints verificando que GET devuelva la consulta correcta | Medio |
| 3 | Realizar pruebas de consultas masivas con diferentes volumenes validando el tiempo de respuesta del listado | Medio |

## HU-003 – Registrar Vehículo
`Story Points: 3`
 
**Justificación SP:** Parecido a HU-001, validaciones múltiples y manejo de varios escenarios de error.
 
### DEV
| # | Tarea |
|---|-------|
| 1 | Crear entidad JPA `Vehiculo` con atributos (marca, modelo, anio, placa) |
| 2 | Implementar repositorio `VehiculoRepository` con validación de unicidad de placa |
| 3 | Crear DTO `VehiculoRequestDTO` y `VehiculoResponseDTO` |
| 4 | Implementar validaciones: campos obligatorios, formato de placa, año numérico positivo |
| 5 | Implementar `POST /api/v1/vehiculos` con respuesta HTTP 201 para creaciones exitosas |
| 6 | Manejar excepción de placa duplicada |
 
### QA
**Justificación SP:** En el rol QA se enfoca en probar las validaciones y casos límite del formato de placa. La complejidad se justifica por las diferentes validaciones que se debe realizar por el formato de la placa en Ecuador
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Diseñar matriz de datos de prueba preparando casos con placas duplicadas, años inválidos (texto, negativos, futuros), campos obligatorios faltantes, y formatos de placa incorrectos | Medio |
| 2 | Escribir tests unitarios del servicio verificando validaciones de placas y formato de datos | Medio |
| 3 | Crear tests de integración del endpoint POST probando el flujo completo de registro incluyendo validaciones| Medio |
| 4 | Ejecutar pruebas exploratorias sobre campos de texto con diferentes combinaciones| Medio |

## HU-004 – Consultar Vehículos
`Story Points: 2`
 
**Justificación SP:** Solo lectura con dos endpoints simples y manejo de un único caso de error.
 
### DEV
| # | Tarea |
|---|-------|
| 1 | Implementar `GET /api/v1/vehiculos` que retorna lista con información básica de cada vehículo |
| 2 | Implementar `GET /api/v1/vehiculos/{id}` que retorna el detalle completo del vehículo |
| 3 | Manejar excepción cuando el vehículo no existe |
 
### QA
**Justificación SP:** Para rol de QA incluye realizar diferentes tipos de test para verificar que las consultas para buscar vehículos se ejecuten de manera correcta.

| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Preparar datos de prueba creando vehículos de diferentes marcas y años para validar| Bajo |
| 2 | Escribir tests de integración verificando que ambos endpoints devuelvan los datos correctos y en el formato esperado | Medio |
| 3 | Validar comportamiento con vehículo inexistente probando que la consulta devuelva 404 | Bajo |

## HU-005: Registrar Póliza de Seguro 
`Story Points: 3` 
### DEV

### QA
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Diseñar matriz de datos de prueba preparando casos con números duplicados, asegurados, vehículos , rangos de fechas validos e inválidos, valores asegurados negativos o cero | Medio |
| 2 | Escribir tests unitarios del servicio verificando todas las validaciones de negocio  | Medio |
|3 | Crear tests de integración probando el flujo completo desde el controller, validando las relaciones con asegurado y vehículo | Alto |
| 4 | Validar cálculo automático del estado verificando que la póliza quede automáticamente en estado ACTIVA posterior al registro | Bajo |
| 5 | Ejecutar pruebas exploratorias de fechas límite probando fechas en el límite y diferentes variantes de fechas | Medio |