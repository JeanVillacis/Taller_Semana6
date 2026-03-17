# PRD: Automatizador de Siniestros - InsurTech

## 1. Visión y Objetivos

### 1.1 Problema que resuelve

Las aseguradoras de autos gestionan mensualmente un alto volumen de reclamos por siniestros. En la mayoría de los casos, estos procesos dependen de revisiones manuales, lo que genera varios inconvenientes:

- **Tiempos de respuesta lentos:** Incluso los siniestros de baja complejidad pueden tardar entre 7 y 30 días hábiles en resolverse, cuando podrían gestionarse en mucho menos tiempo.
- **Costos operativos elevados:** Se destinan recursos humanos a la revisión de casos simples que no necesariamente requieren análisis especializado.
- **Experiencia negativa del cliente:** Los asegurados deben esperar largos periodos para recibir una compensación, lo que impacta negativamente en su percepción del servicio.
- **Inconsistencia en las decisiones:** Las decisiones pueden variar entre diferentes trabajadores, generando inequidad y falta de transparencia.

### 1.2 Visión del producto

Construir una plataforma de evaluación  automatizada de siniestros de autos que transforme el proceso actual de revisión manual en un flujo automatizado capaz de aprobar pagos de bajo riesgo en el menor tiempo posible, escalar a un especialista humano únicamente los casos que presenten indicadores de riesgo , y garantizar la trazabilidad completa de cada decisión para cumplimiento de las pólizas.

### 1.3 Objetivo general

Optimizar el proceso de gestión de reclamos de siniestros de autos automatizando la evaluación y aprobación de casos de bajo riesgo, reduciendo los tiempos de respuesta de días a minutos, liberando al equipo para enfocarse en casos que realmente requieran criterio humano, y garantizando decisiones consistentes y auditables que fortalezcan la confianza del asegurado en el servicio.

### 1.4 Objetivos específicos

- Reducir el tiempo de resolución de siniestros de baja complejidad de un promedio de 7-30 días hábiles a minutos, mediante la aprobación automatizada de reclamos que cumplan con las reglas de bajo riesgo definidas por el negocio, liberando la carga operativa del equipo para que concentren su tiempo en los casos que genuinamente requieran análisis humano.

- Estandarizar las decisiones de evaluación a través de un motor de reglas de negocio configurable que elimine la variabilidad entre revisores, asegurando que reclamos con las mismas características reciban siempre el mismo tratamiento.

- Garantizar la trazabilidad completa de cada decisión (automática o manual), registrando las reglas evaluadas, las banderas detectadas y la justificación de cada resolución.


### 1.5 Usuarios objetivo

| Usuario | Descripción | Necesidad principal |
|---------|-------------|---------------------|
| **Asegurado** | Persona con póliza de auto activa que sufre un siniestro | Registrar su reclamo y consultar el estado de su resolución |
| **Gestor** | Empleado que administra pólizas y resuelve reclamos escalados | Gestionar vehículos y pólizas (CRUD completo), y resolver los casos que levanten banderas rojas con contexto claro |
| **Administrador del Sistema** | Responsable de configurar reglas de negocio | Ajustar umbrales y reglas de evaluación sin necesidad de despliegue técnico |

## 2. Alcance del MVP

### 2.1 IN (Incluido en la primera versión)
1. **Gestion completa de asegurados (CRUD):** El gestor puede registrar, consultar, actualizar y eliminar asegurados (nombre, apellido, número de identificación, dirección, teléfono, correo electrónico).

2. **Gestión completa de vehículos (CRUD):** El gestor puede registrar, consultar, actualizar y eliminar vehículos para asegurar (marca, modelo, año, placa).

3. **Gestión completa de pólizas (CRUD):** El gestor puede registrar, consultar, actualizar y eliminar pólizas de seguro (número, asegurado, valor asegurado, vigencia), vinculándolas a vehículos previamente registrados.

4. **Registro de reclamo de siniestro:** El asegurado registra un reclamo proporcionando datos del incidente (fecha, descripción, monto estimado,ubicación, fotografías). El sistema asigna un número de seguimiento único.

5. **Validación automática de póliza y evaluación por reglas de negocio:** El sistema verifica que la póliza esté activa. Si la póliza no es válida, el reclamo se rechaza con motivo claro. Si es válida, aplica las siguientes reglas:

   - **Regla de monto:** Si el monto estimado es ≤ al deducible mínimo → no procede como reclamo, se descarta. Si es > al deducible mínimo y < 20% del valor asegurado → candidato a aprobación automática. Si es ≥ 20% del valor asegurado → bandera roja, revisión manual.
   El deducible se calcula como el mayor entre: 10% del monto del siniestro, 1% del valor asegurado, y $200.
   - **Regla de historial:** Si el asegurado tiene 0 siniestros en los últimos 12 meses → candidato a aprobación automática. Si tiene ≥ 2 siniestros en los últimos 12 meses → bandera roja, revisión manual.
   - **Regla de antigüedad de póliza:** Si la póliza tiene ≥ 30 días de vigencia → candidato a aprobación automática. Si tiene < 30 días → bandera roja, se envía a revisión manual.

**Nota:** Se realizo una investigación de las reglas de negocio de las principales aseguradoras del Ecuador y se determino que las reglas definidas son las mas adecuadas para el MVP.

6. **Panel del gestor de seguros:** El gestor puede ver los reclamos escalados de un siniestro con sus banderas rojas, y registrar su resolución (aprobar/rechazar) con justificación. Adiconalmente puede ver información del asegurado.

7. **Consulta de estado:** El asegurado puede consultar en cualquier momento el estado actual de su reclamo (aprobado, en revisión, rechazado) y el motivo de la decisión.

### 2.2 OUT (Excluido del MVP)

- Ajustes de las reglas del negocio, realizado por el administrador.
- Generar reportes de trazabilidad de los reclamos.
- Gestión de pagos y transferencias bancarias reales (se notifica la aprobación).
- Reportería avanzada y dashboards analíticos.