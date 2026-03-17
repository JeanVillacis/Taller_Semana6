Historias Técnicas y de Arquitectura

HT-001: Configuración del Proyecto Base
COMO arquitecto de software
QUIERO configurar el esqueleto del proyecto con el stack definido
PARA tener un entorno estandarizado desde donde el equipo pueda empezar a trabajar

Stack: Java 17+, Spring Boot (Web, Data JPA, Validation), Docker + docker-compose

Criterios de Aceptación
-Proyecto base
-El proyecto compila sin errores

Docker
Existe un docker-compose.yml que levanta la aplicación

Configuración base
Health check
GET /api/health responde HTTP 200 OK

HT-002: Diseño y Creación de la Base de Datos
COMO desarrollador backend
QUIERO diseñar el esquema relacional en PostgreSQL e implementar las entidades en el código
PARA persistir de forma segura los datos de asegurados, vehículos, pólizas y siniestros

Stack: PostgreSQL, Hibernate / Spring Data JPA

Tablas principales:
-asegurados: id, nombre, apellido, numero_identificacion, direccion, telefono, correo_electronico
-vehiculos: id, marca, modelo, anio, placa, chasis, motor
-polizas: id, numero, asegurado_id, vehiculo_id, valor_asegurado, vigencia_inicio, vigencia_fin, estado
-reclamos: id, poliza_id, fecha_incidente, descripcion, monto_estimado, ubicacion, estado, resolucion, justificacion, numero_seguimiento
-reclamo_fotografias: id, reclamo_id, url_fotografia
-reclamo_banderas: id, reclamo_id, descripcion_bandera

Criterios de Aceptación

Docker
El docker-compose.yml incluye el contenedor de PostgreSQL con sus variables de entorno

Conexión
La aplicación se conecta exitosamente a la base de datos al arrancar

Esquema
Las entidades JPA generan la estructura de tablas correcta al iniciar

Integridad referencial
No se puede eliminar un asegurado si tiene pólizas vinculadas