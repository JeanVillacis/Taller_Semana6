# Historias de Usuario - Evaluador Automatizado de Siniestros

---

## HU-001 – Registro de asegurado


**Como** gestor de seguros,  
**Quiero** registrar los datos personales de un asegurado en el sistema,  
**Para** que pueda ser vinculado a un vehículo y una póliza de seguro.

**Prioridad:** Alta  
**Story Points:** 3


### Criterios de aceptación

#### Escenario 1: Registro correcto
```gherkin
Dado que el gestor está autenticado en el sistema
Cuando registra un asegurado con todos los datos requeridos (nombre, apellido, identificación, dirección, teléfono 
y correo electrónico)
Entonces el sistema guarda el asegurado correctamente
Y queda disponible para ser usado en una póliza o vehículo
```

#### Escenario 2:  Faltan datos obligatorios
```gherkin
Dado que el gestor está autenticado en el sistema
Cuando intenta registrar un asegurado sin completar todos los campos obligatorios
Entonces el sistema no permite guardar el registro
Y muestra qué campos faltan
```

#### Escenario 3: Identificación registrada previamente
```gherkin
Dado que ya existe un asegurado con una identificación registrada
Cuando el gestor intenta registrar otro asegurado con la misma identificación
Entonces el sistema no permite guardar el registro
Y muestra un mensaje indicando que ya existe
```

#### Escenario 4: Correo electrónico formato inválido
```gherkin
Dado que el gestor está autenticado en el sistema
Cuando ingresa un correo con formato inválido
Entonces el sistema no permite guardar el registro
Y muestra un mensaje indicando el error en el correo
```

## HU-002: Consultar Asegurados

**Como** gestor de seguros,
**Quiero** consultar asegurados registrados en el sistema, tanto en listado como en detalle individual,
**Para** verificar su información antes de vincularlos a pólizas o vehículos.

**Prioridad:** Alta  
**Story Points:** 2


### Criterios de Aceptación (Gherkin)

#### Escenario 1: Consulta de listado de asegurados
```gherkin
Dado que soy un gestor autenticado en el sistema
Y existen asegurados registrados
Cuando consulto la lista de asegurados
Entonces visualizo un listado con la información de identificación básica de cada asegurado
```
#### Escenario 2: Consulta del detalle de un asegurado específico
```gherkin
Dado que soy un gestor autenticado en el sistema
Y existe un asegurado registrado en el sistema
Cuando consulto el detalle de ese asegurado
Entonces visualizo toda la información disponible para ese asegurado
```

#### Escenario 3: Consulta de un asegurado inexistente
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando intento consultar el detalle de un asegurado que no existe en el sistema
Entonces el sistema me informa que no se encontró ningún asegurado con ese criterio
Y no se muestra información parcial ni de otro asegurado
```



## Historias Técnicas y de Arquitectura


### HT-001: Configuración del Proyecto Base

**Como** arquitecto de software
**Quiero** configurar el esqueleto del proyecto con el stack definido
**Para** que el equipo pueda empezar a trabajar sobre una base común

**Stack:** Java 17+, Spring Boot (Web, Data JPA, Validation), Docker + docker-compose

**Criterios de Aceptación**

- El proyecto compila sin errores
- Existe un `docker-compose.yml` que levanta la aplicación
- Incluye manejo global de excepciones (Controller Advice)
- `GET /api/health` responde HTTP 200 OK

---

### HT-002: Diseño de la Base de Datos

**Como** desarrollador backend
**Quiero** implementar el esquema relacional en PostgreSQL con sus entidades JPA
**Para** persistir los datos del sistema de forma estructurada

**Stack:** PostgreSQL, Hibernate / Spring Data JPA

**Tablas principales:**
- `asegurados` — id, nombre, apellido, numero_identificacion, direccion, telefono, correo_electronico
- `vehiculos` — id, marca, modelo, anio, placa, chasis, motor
- `polizas` — id, numero, asegurado_id, vehiculo_id, valor_asegurado, vigencia_inicio, vigencia_fin, estado
- `reclamos` — id, poliza_id, fecha_incidente, descripcion, monto_estimado, ubicacion, estado, resolucion, justificacion, numero_seguimiento
- `reclamo_fotografias` — id, reclamo_id, url_fotografia
- `reclamo_banderas` — id, reclamo_id, descripcion_bandera

**Criterios de Aceptación**

- El `docker-compose.yml` incluye el contenedor de PostgreSQL configurado

- La aplicación se conecta a la base de datos al arrancar

- Las tablas se generan correctamente al iniciar

- No se puede eliminar un asegurado con pólizas vinculadas

---

### HT-003: Endpoints REST

**Como** desarrollador backend
**Quiero** crear los controladores REST para las entidades del MVP
**Para** soportar las operaciones CRUD y el flujo completo de reclamos

**Endpoints principales:**
CRUD completo en `/api/v1/asegurados`, `/api/v1/vehiculos` y `/api/v1/polizas`

Reclamos:
- `POST /api/v1/reclamos` — registrar reclamo
- `GET /api/v1/reclamos/{numeroSeguimiento}/estado` — consultar estado
- `POST /api/v1/reclamos/{numeroSeguimiento}/resolucion` — aprobar o rechazar con justificación
- `PUT /api/v1/reclamos/{numeroSeguimiento}/estado` — actualizar estado del reclamo

**Criterios de Aceptación**

- Existen controllers para todas las entidades
- Los endpoints de reclamos cubren el ciclo completo: registro, consulta, escalado y resolución
- Los endpoints validan campos obligatorios y responden en JSON
- Respuestas exitosas devuelven HTTP 200 o 201
- Respuestas erróneas devuelven HTTP 400 o 404 con mensaje descriptivo

### HT-004: Seguridad y Control de Acceso

**Como** arquitecto de software
**Quiero** implementar autenticación y autorización en la API
**Para** que solo usuarios autenticados puedan operar según su rol

**Stack:** Spring Security, JWT

**Roles:**
- `GESTOR` — acceso completo a vehículos, pólizas, asegurados y resolución de reclamos
- `ASEGURADO` — solo puede registrar y consultar sus propios reclamos
- `ADMIN` — acceso total incluyendo configuración del sistema

**Criterios de Aceptación**

- Los endpoints protegidos rechazan peticiones sin token válido con HTTP 401
- Un usuario no puede operar sobre recursos de otro rol con HTTP 403
- El token JWT expira y no puede reutilizarse una vez vencido
- Existe un endpoint `POST /api/v1/auth/login` que devuelve el token