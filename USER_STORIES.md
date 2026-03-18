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

## HU-003: Registrar Vehículo

**Como** gestor de seguros,  
**Quiero** registrar los datos de un vehículo en el sistema,  
**Para** que pueda ser asociado a una póliza de seguro.

**Prioridad:** Alta  
**Story Points:** 3



### Criterios de Aceptación (Gherkin)

#### Escenario 1: Registro exitoso de vehículo con datos completos
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando registro un vehículo proporcionando todos los campos obligatorios (marca, modelo, año y placa) con valores válidos
Y la placa del vehículo no existe previamente en el sistema
Entonces el sistema confirma que el vehículo fue registrado exitosamente
Y el vehículo queda disponible para ser asociado a una póliza
```

#### Escenario 2: Intento de registro con datos obligatorios faltantes
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando intento registrar un vehículo sin completar uno o más campos obligatorios
Entonces el sistema rechaza el registro
Y me indica cuáles son los campos obligatorios que faltan por completar
```

#### Escenario 3: Intento de registro con placa duplicada
```gherkin
Dado que soy un gestor autenticado en el sistema
Y ya existe un vehículo registrado con una placa determinada
Cuando intento registrar otro vehículo con esa misma placa
Entonces el sistema rechaza el registro
Y me informa que ya existe un vehículo registrado con esa placa
Y no se crea ningún registro nuevo en el sistema
```

#### Escenario 4: Intento de registro con formato de datos inválidos
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando intento registrar un vehículo con un campo que no cumple el formato esperado
Entonces el sistema rechaza el registro
Y me indica qué campo contiene el error y por qué el valor no es válido
Y no se crea ningún registro nuevo en el sistema
```

## HU-004: Consultar Vehículos

**Como** gestor de seguros,  
**Quiero** consultar la lista de vehículos y ver el detalle de uno específico,  
**Para** verificar datos antes de asociar una póliza.

**Prioridad:** Alta  
**Story Points:** 2

### Criterios de Aceptación (Gherkin)

#### Escenario 1: Consulta de listado de vehículos
```gherkin
Dado que soy un gestor autenticado en el sistema
Y existen vehículos registrados en el sistema
Cuando consulto la lista de vehículos
Entonces visualizo un listado con la información de identificación básica de cada vehículo
```

#### Escenario 2: Consulta de un vehículo existente
```gherkin
Dado que soy un gestor autenticado en el sistema
Y existe un vehículo registrado en el sistema
Cuando consulto el detalle de ese vehículo
Entonces visualizo toda la información disponible para ese vehículo
```

#### Escenario 3: Consulta de un vehículo no existente
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando intento consultar el detalle de un vehículo que no existe en el sistema
Entonces el sistema me informa que no se encontró ningún vehículo con ese criterio
Y no se muestra información parcial ni de otro vehículo
```

## HU-005: Registrar Póliza de Seguro

**Como** gestor de seguros,  
**Quiero** registrar una póliza asociándola a un asegurado y a un vehículo previamente registrados,  
**Para** que el asegurado pueda presentar reclamos contra esa póliza.

**Prioridad:** Alta  
**Story Points:** 3

### Criterios de Aceptación (Gherkin)

#### Escenario 1: Registro exitoso de póliza con datos completos y válidos
```gherkin
Dado que soy un gestor autenticado en el sistema
Y existe un vehículo registrado en el sistema
Y existe un asegurado registrado en el sistema
Y el número de póliza no existe previamente en el sistema
Cuando registro una póliza proporcionando todos los campos obligatorios con valores válidos
Entonces el sistema confirma que la póliza fue registrada exitosamente
Y la póliza queda vinculada al vehículo y al asegurado indicados
Y la póliza toma el estado ACTIVA
```

#### Escenario 2: Registro de póliza a un vehículo inexistente
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando intento registrar una póliza asociada a un vehículo que no existe en el sistema
Entonces el sistema rechaza el registro
Y me informa que el vehículo indicado no se encuentra registrado
Y no se crea ningún registro de póliza en el sistema
```

#### Escenario 3: Intento de registro con número de póliza duplicado
```gherkin
Dado que soy un gestor autenticado en el sistema
Y ya existe una póliza registrada con un número determinado
Cuando intento registrar otra póliza con ese mismo número
Entonces el sistema rechaza el registro
Y me informa que ya existe una póliza registrada con ese número
Y no se crea ningún registro nuevo en el sistema
```

#### Escenario 4: Intento de registro con rango de vigencia inválido
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando intento registrar una póliza con una fecha de fin anterior o igual a la fecha de inicio
Entonces el sistema rechaza el registro
Y me indica que el rango de vigencia no es válido
Y no se crea ningún registro de póliza en el sistema
```
## HU-006: Consultar Pólizas

**Como** gestor de seguros,  
**Quiero** consultar pólizas registradas y ver el detalle de una específica,  
**Para** verificar estado, vigencia y vehículo asociado.

**Prioridad:** Alta  
**Story Points:** 2

### Criterios de Aceptación (Gherkin)

#### Escenario 1: Consulta de listado
```gherkin
Dado que soy un gestor autenticado en el sistema
Y existen pólizas registradas en el sistema
Cuando consulto la lista de pólizas
Entonces visualizo un listado con la información de identificación básica de cada póliza
```

#### Escenario 2: Consulta del detalle de una póliza existente
```gherkin
Dado que soy un gestor autenticado en el sistema
Y existe una póliza registrada en el sistema
Cuando consulto el detalle de esa póliza
Entonces visualizo toda la información disponible para esa póliza
Y puedo identificar el vehículo y el asegurado vinculados a ella
```

#### Escenario 3: Consulta de una póliza no existente
```gherkin
Dado que soy un gestor autenticado en el sistema
Cuando intento consultar el detalle de una póliza que no existe en el sistema
Entonces el sistema me informa que no se encontró ninguna póliza con ese criterio
Y no se muestra información de la poliza.
```

## HU-007: Registro de Reclamo de Siniestro

**Como** asegurado con una póliza de auto activa,  
**Quiero** registrar un reclamo de siniestro proporcionando los datos del incidente y fotografías en png o jpg,  
**Para** iniciar el proceso de evaluación y obtener una respuesta sobre mi compensación.

**Prioridad:** Alta  
**Story Points:** 5

### Criterios de Aceptación (Gherkin)

#### Escenario 1: Registro exitoso con datos completos y válidos
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y tengo una póliza activa y vigente
Cuando registro un reclamo proporcionando todos los campos obligatorios con valores válidos
Y adjunto al menos una fotografía en formato png o jpg
Entonces el sistema confirma que el reclamo fue registrado exitosamente
Y el reclamo toma el estado REGISTRADO
Y el sistema me asigna un número de seguimiento único para ese reclamo
```

#### Escenario 2: Intento de registro sin seleccionar una póliza activa
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y no tengo ninguna póliza activa y vigente disponible para seleccionar
Cuando intento acceder al formulario de registro de reclamo
Entonces el sistema me informa que no es posible registrar reclamos sin una póliza activa y vigente
Y no se crea ningún registro de reclamo en el sistema
```

#### Escenario 3: Intento de registro con campos obligatorios faltantes
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y tengo una póliza activa y vigente
Cuando intento registrar un reclamo sin completar uno o más campos obligatorios
Entonces el sistema rechaza el registro
Y me indica cuáles son los campos obligatorios que faltan por completar
Y no se crea ningún registro de reclamo en el sistema
```

#### Escenario 4: Intento de registro con monto estimado inválido
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y tengo una póliza activa y vigente
Cuando intento registrar un reclamo con un monto estimado menor o igual a cero
Entonces el sistema rechaza el registro
Y me indica que el monto estimado debe ser un valor positivo
Y no se crea ningún registro de reclamo en el sistema
```

#### Escenario 5: Intento de registro con fecha de incidente fuera del período de vigencia
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y tengo una póliza activa y vigente
Cuando intento registrar un reclamo con una fecha de incidente posterior a la fecha actual o anterior al inicio de vigencia de la póliza
Entonces el sistema rechaza el registro
Y me indica que la fecha del incidente debe estar dentro del período de vigencia de la póliza y no puede ser futura
Y no se crea ningún registro de reclamo en el sistema
```

#### Escenario 6: Registro exitoso con fotografías válidas en formato permitido
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y tengo una póliza activa y vigente
Cuando registro un reclamo adjuntando fotografías en formato png o jpg
Entonces el sistema acepta las fotografías y las asocia al reclamo
Y el reclamo se registra exitosamente con las evidencias adjuntas
```

#### Escenario 7: Intento de registro con fotografías en formato no permitido
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y tengo una póliza activa y vigente
Cuando intento registrar un reclamo adjuntando archivos en un formato distinto a png o jpg
Entonces el sistema rechaza los archivos adjuntos
Y me indica que solo se permiten fotografías en formato png o jpg
Y no se crea ningún registro de reclamo en el sistema
```

#### Escenario 8: Intento de registro sin adjuntar fotografías
```gherkin
Dado que soy un asegurado autenticado en el sistema
Y tengo una póliza activa y vigente
Cuando intento registrar un reclamo sin adjuntar ninguna fotografía
Entonces el sistema rechaza el registro
Y me indica que es obligatorio adjuntar al menos una fotografía como evidencia del siniestro
Y no se crea ningún registro de reclamo en el sistema
```
## HU-008: Validación de póliza para procesamiento de reclamo

**Como** sistema de evaluación de siniestros,  
**Quiero** validar automáticamente la elegibilidad de la póliza al momento de procesar un reclamo,  
**Para** descartar de inmediato los reclamos que no cumplen con las condiciones de la poliza

**Prioridad:** Alta  
**Story Points:** 5

### Criterios de Aceptación (Gherkin)

#### Escenario 1: Rechazo por póliza no vigente
```gherkin
Dado que existe un reclamo registrado en el sistema
Y la póliza asociada a ese reclamo no está activa ni vigente
Cuando el sistema ejecuta la validación de elegibilidad de la póliza
Entonces el reclamo queda en estado de rechazo
Y se registra el motivo correspondiente a póliza no vigente
Y no se continúa con ninguna evaluación adicional sobre ese reclamo
```

#### Escenario 2: Escalamiento por antigüedad insuficiente de la póliza
```gherkin
Dado que existe un reclamo registrado en el sistema
Y la póliza asociada está activa y vigente
Y la póliza tiene una antigüedad menor a 30 días desde su fecha de inicio de vigencia
Cuando el sistema ejecuta la validación de elegibilidad de la póliza
Entonces el reclamo se escala a revisión manual
Y se registra la bandera correspondiente a antigüedad insuficiente (menor a 30 días)
Y no se continúa con la evaluación por reglas de monto e historial
```

#### Escenario 3: Póliza elegible — Continúa a evaluación por reglas
```gherkin
Dado que existe un reclamo registrado en el sistema
Y la póliza asociada está activa, vigente y con antigüedad igual o mayor a 30 días
Cuando el sistema ejecuta la validación de elegibilidad de la póliza
Entonces el reclamo queda habilitado para continuar con la evaluación por reglas de la poliza
Y no se registra ninguna bandera ni motivo de rechazo en esta fase
```
## HU-009: Evaluación de reclamo por reglas de deducible y monto

**Como** sistema de evaluación de siniestros,  
**Quiero** evaluar automáticamente cada reclamo elegible aplicando las reglas de deducible y monto respecto al valor asegurado,  
**Para** resolver sin intervención manual los reclamos de bajo riesgo por monto y escalar los que superen el umbral definido.

**Prioridad:** Alta  
**Story Points:** 5

**Nota:** El deducible se calcula como el mayor entre: 10% del monto del siniestro, 1% del valor asegurado y $200. El umbral de escalamiento por monto es el 20% del valor asegurado (según reglas definidas en el PRD sección 2.1).

### Criterios de Aceptación (Gherkin)

#### Escenario 1: Descarte por monto menor o igual al deducible calculado
```gherkin
Dado que existe un reclamo elegible para evaluación
Y el monto estimado del reclamo es menor o igual al deducible calculado (el mayor entre 10% del monto del siniestro, 1% del valor asegurado y $200)
Cuando el motor de reglas evalúa el reclamo
Entonces el reclamo queda en estado de descarte
Y se registra el motivo indicando que el monto no supera el deducible aplicable
```

#### Escenario 2: Aprobación automática por monto dentro del rango permitido
```gherkin
Dado que existe un reclamo elegible para evaluación
Y el monto estimado supera el deducible calculado
Y el monto estimado es menor al 20% del valor asegurado
Cuando el motor de reglas evalúa el reclamo
Entonces el reclamo continúa a la evaluación por historial de siniestros (HU-010)
Y no se registra ninguna bandera de escalamiento por monto
```

#### Escenario 3: Escalamiento por monto que supera el umbral del valor asegurado
```gherkin
Dado que existe un reclamo elegible para evaluación
Y el monto estimado supera el deducible calculado
Y el monto estimado es igual o mayor al 20% del valor asegurado
Cuando el motor de reglas evalúa el reclamo
Entonces el reclamo se escala a revisión manual
Y se registra la bandera correspondiente al monto elevado respecto al valor asegurado
```

## HU-010: Evaluación de reclamo por historial de siniestros

**Como** sistema de evaluación de siniestros,  
**Quiero** evaluar el historial de siniestros recientes del asegurado para los reclamos que pasaron la validación de monto,  
**Para** aprobar automáticamente los reclamos sin indicadores de riesgo por historial y escalar los que presenten frecuencia elevada.

**Prioridad:** Alta  
**Story Points:** 3


### Criterios de Aceptación (Gherkin)

#### Escenario 1: Aprobación automática sin banderas de historial
```gherkin
Dado que existe un reclamo que pasó la evaluación de monto sin banderas
Y el asegurado tiene 0 siniestros registrados en los últimos 12 meses
Cuando el motor de reglas evalúa el historial del asegurado
Entonces el reclamo queda aprobado automáticamente
Y se registra el monto aprobado y el deducible aplicado
```

#### Escenario 2: Escalamiento por historial de siniestros recientes
```gherkin
Dado que existe un reclamo que pasó la evaluación de monto sin banderas
Y el asegurado tiene 2 o más siniestros registrados en los últimos 12 meses
Cuando el motor de reglas evalúa el historial del asegurado
Entonces el reclamo se escala a revisión manual
Y se registra la bandera correspondiente al historial de siniestros recientes
```

#### Escenario 3: Escalamiento por múltiples banderas activas simultáneas
```gherkin
Dado que existe un reclamo elegible para evaluación
Y el reclamo activa más de una bandera de escalamiento (monto e historial)
Cuando el motor de reglas evalúa el reclamo
Entonces el reclamo se escala a revisión manual
Y se registran todas las banderas activas que motivaron el escalamiento
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