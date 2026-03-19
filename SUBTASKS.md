# Historias Técnicas

## HT-001 – Configuración del Proyecto Base
`Story Points: 2`

**Justificación SP:** Infraestructura base sin lógica de negocio, pero es la base del proyecto y requiere configuración de entorno.


### DEV
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Inicializar proyecto Spring Boot con dependencias: Web, Data JPA, Validation, Security y JWT| Medio |
| 2 | Configurar `application.properties` con las variables de entorno para la conexión a la BD | Bajo |
| 3 | Crear `Dockerfile` para la aplicación Spring Boot | Bajo |
| 4 | Crear `docker-compose.yml` que levante la aplicación Spring Boot | Bajo |
| 5 | Implementar endpoint `GET /api/health` | Bajo |
 
### QA
| # | Tarea |
|---|-------|
| --- | --- |



## HT-002 – Diseño de la Base de Datos
`Story Points: 3`

**Justificación SP:** Define el esquema completo del sistema con relaciones entre múltiples entidades y constraints de integridad referencial.

### DEV
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Definir entidades JPA: `Asegurado`, `Vehiculo`, `Poliza`, `Reclamo`, `ReclamoFotografia`, `ReclamoBandera` | Alto |
| 2 | Configurar relaciones `@OneToMany` y `@ManyToOne` entre entidades | Medio |
| 3 | Agregar contenedor PostgreSQL al `docker-compose.yml` con variables de entorno | Bajo |
| 4 | Configurar `spring.jpa.hibernate.ddl-auto` en `application.properties` para la generación automática de tablas | Bajo |
| 5 | Agregar constraint de integridad referencial: no eliminar asegurado con póliz
### QA
| # | Tarea |
|---|-------|
| --- | --- |



## HT-003 – Seguridad y Control de Acceso
`Story Points: 5`

**Justificación SP:** Involucra Spring Security, JWT, filtros de autenticación y control de acceso por roles.

### DEV
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Crear entidad `Usuario` con atributos (email, password, rol) | Bajo |
| 2 | Implementar repositorio `UsuarioRepository` | Bajo |
| 3 | Implementar `POST /api/v1/auth/login` que valida credenciales y retorna token JWT | Alto |
| 4 | Implementar filtro JWT para validar token en cada request protegido | Alto |
| 5 | Configurar `SecurityFilterChain` con reglas por rol: GESTOR, ASEGURADO | Medio |
| 6 | Hashear contraseñas antes de guardarlas | Bajo |
 
### QA
| # | Tarea |
|---|-------|
| --- | --- |



# Historias de Usuario

## HU-001 – Registro de Asegurado
`Story Points: 3`

**Justificación SP:** Validaciones múltiples y manejo de varios escenarios de error.

### DEV
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Crear entidad JPA `Asegurado` con sus atributos (nombre, apellido, numeroIdentificacion, direccion, telefono, correoElectronico) | Bajo |
| 2 | Implementar repositorio `AseguradoRepository` | Bajo |
| 3 | Implementar validaciones de unicidad de identificacion y correo | Medio |
| 4 | Crear DTO `AseguradoDTO` | Bajo |
| 5 | Crear service `AseguradoService` con la logica de negocio para registrar asegurados | Medio |
| 6 | Implementar `POST /api/v1/asegurados` en el controller | Medio |
 
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
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Implementar `GET /api/v1/asegurados` que retorna lista con información básica de cada asegurado | Bajo |
| 2 | Implementar `GET /api/v1/asegurados/{id}` que retorna el detalle completo del asegurado | Bajo |
| 3 | Manejar excepción cuando el asegurado no existe | Bajo |
 
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
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Crear entidad JPA `Vehiculo` con atributos (marca, modelo, anio, placa) | Bajo |
| 2 | Implementar repositorio `VehiculoRepository` con validación de unicidad de placa | Bajo |
| 3 | Crear DTO `VehiculoRequestDTO` y `VehiculoResponseDTO` | Bajo |
| 4 | Implementar validaciones: campos obligatorios, formato de placa, año numérico positivo | Medio |
| 5 | Implementar `POST /api/v1/vehiculos` con respuesta HTTP 201 para creaciones exitosas | Medio |
| 6 | Manejar excepción de placa duplicada | Bajo |
 
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
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Implementar `GET /api/v1/vehiculos` que retorna lista con información básica de cada vehículo | Bajo |
| 2 | Implementar `GET /api/v1/vehiculos/{id}` que retorna el detalle completo del vehículo | Bajo |
| 3 | Manejar excepción cuando el vehículo no existe | Bajo |
 
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
**Justificación SP:** Para rol QA se concentra en probar todas las combinaciones de validaciones y relaciones, requiriendo tests de integración complejos.
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Diseñar matriz de datos de prueba preparando casos con números duplicados, asegurados, vehículos , rangos de fechas validos e inválidos, valores asegurados negativos o cero | Medio |
| 2 | Escribir tests unitarios del servicio verificando todas las validaciones de negocio  | Medio |
|3 | Crear tests de integración probando el flujo completo desde el controller, validando las relaciones con asegurado y vehículo | Alto |
| 4 | Validar cálculo automático del estado verificando que la póliza quede automáticamente en estado ACTIVA posterior al registro | Bajo |
| 5 | Ejecutar pruebas exploratorias de fechas límite probando fechas en el límite y diferentes variantes de fechas | Medio |

## HU-006: Consultar Pólizas
`Story Points: 2`
### DEV

### QA
**Justificación SP:** Para rol de QA se enfoca en validar la consultas correctas obteniendo información completa de las polizas.

| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Preparar datos de prueba creando pólizas con diferentes estados (ACTIVA, INACTIVA) y fechas  para validar consultas | Bajo |
| 2 | Escribir tests de integración verificando que los endpoints devuelvan correctamente la información de la póliza| Alto |
| 3 | Validar comportamiento con póliza inexistente, esperando un 404 | Bajo |
| 4 | Verificar carga de relaciones asegurando que no haya problemas al realizar varias consultas | Medio |

## HU-007: Registro de Reclamo de Siniestro
`Story Points: 5`
### DEV

### QA
**Justificación SP:** Para rol QA el esfuerzo es alto porque requiere probar múltiples escenarios de archivos, validar la transaccionalidad y asegurar que no haya casos límite sin cubrir.

| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Diseñar matriz de datos de prueba preparando casos con pólizas inactivas, fechas futuras, montos cero o negativos, fotografías en formatos incorrectos, sin fotografías | Medio |
| 2 | Escribir tests unitarios del servicio verificando todas las validaciones y número de seguimiento | Alto |
| 3 | Crear tests de integración del endpoint probando el flujo completo incluyendo la subida de fotografias | Alto |
| 4 | Validar almacenamiento de fotografías verificando que las fotografías se guarden correctamente | Medio |
| 5 | Probar límites de tamaño del tamaño de los archivos de fotografías, validando los posibles casos | Medio |
| 6 | Realizar pruebas exploratorias de formatos de imagen probando con archivos, con extensión cambiada diferente | Medio |
| 7 | Validar mensajes de error descriptivos asegurando que cada tipo de error devuelva un mensaje claro  | Medio |

## HU-008: Validación de póliza para procesamiento de reclamo 
`Story Points: 5`
### DEV
### QA
**Justificación SP:** Para rol QA el esfuerzo  es alto porque requiere probar cada regla de forma aislada y en combinación de validar la póliza.
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Diseñar casos de prueba para cada regla preparando datos con pólizas inactivas, vencidas, con antigüedad definidas en las reglas de las polizas | Medio |
| 2 | Escribir tests unitarios de cada regla probando las reglas de forma aislada con diferentes estados de póliza y fechas | Alto |
| 3 | Crear tests de integración del flujo completo verificando que al registrar un reclamo | Alto |
| 4 | Validar que se registren las banderas correctamente verificando que cuando un reclamo se escala| Medio |
| 5 | Probar casos límite de fechas validas al regustrar un reclamo | Medio |

## HU-009: Evaluación de reclamo por reglas de deducible y monto
`Story Points: 5`
### DEV
### QA
**Justificación SP:** Para rol QA es alto porque requiere probar  los casos límite y la precisión de los cálculos , especialmente dado que son cálculos financieros. 
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Diseñar casos de prueba para el cálculo del deducible preparando escenarios con diferentes tipos de condiciones| Medio |
|2 | Crear tests unitarios del cálculo del deducible verificando con diferentes combinaciones  | Medio |
| 3 | Escribir tests para la regla de descarte probando casos donde el monto es menor, igual o mayor al deducible | Medio |
| 4 | Escribir tests para la regla de monto elevado probando casos diferentes de montos | Medio |
| 5 | Crear tests de integración del flujo completo verificando que un reclamo pase por todas las validaciones | Alto |
| 6 | Validar casos límite de montos probando con montos exactamente iguales y variados para evaluar reclamos | Medio |

##  HU-010: Evaluación de reclamo por historial de siniestros 
`Story Points: 3`

### DEV
### QA
**Justificación SP:** Para rol QA se enfoca en probar combinaciones de historial y verificar el flujo end-to-end desde el registro hasta la aprobación. 
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Diseñar casos de prueba para historial preparando escenarios diferentes| Medio |
| 2 | Escribir tests unitarios de la consulta de historial verificando que el conteo de siniestros en rango de fechas | Medio |
| 3 | Crear tests para la regla de historial sin siniestros y aprovación | Medio |
| 4 | Crear tests para la regla de historial con banderas de siniestros| Medio |
| 5 | Validar el flujo completo de aprobación automática verificando que un reclamo que pasa todas las reglas  | Alto |
##  HU-011: Panel del gestor de seguros
`Story Points: 3`

### DEV
### QA
**Justificación SP:** El esfuerzo del rol QA se concentra en validar la autorizacióny la integridad de los datos complejos. .
| # | Tarea | Esfuerzo |
|---|-------|----------|
| 1 | Preparar datos de prueba con reclamos escalados creando múltiples reclamos en estado de revisión manual | Medio |
| 2 | Escribir tests de integración del endpoint de listado verificando que el endpoint devuelva correctamente los reclamos  | Medio |
| 3 | Ejecutar pruebas exploratorias del panel navegando manualmente por el panel verificando que todos los datos se muestren correctamente | Medio |

