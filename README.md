Protecto PSet 2

# PSet #2 - Data Engineering: NY Taxi Pipeline

**Autor:** [Tu Nombre/Tefo]
[cite_start]**Curso:** Fundamentos de Ciencia de Datos - Universidad San Francisco de Quito [cite: 1-3]


## 1. Objetivo del Proyecto
[cite_start]El objetivo de este proyecto es construir una solución end-to-end con enfoque ELT (Extract, Load, Transform) para ingerir, almacenar, transformar y modelar datos históricos de NY Taxi (período 2015-2025)[cite: 5, 13]. [cite_start]Se busca diseñar una arquitectura reproducible orquestada con Mage, utilizando PostgreSQL como data warehouse y pgAdmin como herramienta de inspección[cite: 6].

## 2. Arquitectura
[cite_start]La infraestructura está completamente dockerizada y consta de tres servicios principales conectados mediante una red interna (bridge) y con persistencia de datos mediante volúmenes [cite: 25-27, 36-39]:
* **Orquestador:** Mage AI (Puerto 6789)
* **Data Warehouse:** PostgreSQL 15 (Puerto 5432)
* **Interfaz de BD:** pgAdmin 4 (Puerto 9000)

[cite_start]*La gestión de credenciales y configuraciones sensibles se maneja estrictamente mediante variables de entorno en un archivo `.env` y el archivo `io_config.yaml` de Mage (Secrets) [cite: 10, 115-127].*

## 3. Pasos para levantar el entorno
Para desplegar la infraestructura local de manera reproducible [cite: 31-33]:
1. Clonar el repositorio.
2. Crear un archivo `.env` en la raíz del proyecto basándose en el `.env.example` (definiendo `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, etc.).
3. Ejecutar en la terminal:
   ```bash
   docker-compose up -d

Acceder a Mage ingresando a http://localhost:6789 en el navegador.

Ir a la sección Pipelines.


Pipeline 1 (raw_ingestion_pipeline): Encargado de leer los datos fuente en formato Parquet y cargarlos de forma inmutable al esquema raw .


Pipeline 2 (clean_transformation_pipeline): Lee desde la capa raw, limpia los datos y construye el modelo dimensional en el esquema clean .
Nota: Los pipelines cuentan con triggers configurados para su ejecución secuencial y automatizada

Ingresar a http://localhost:9000 en el navegador.
Iniciar sesión con el correo y contraseña definidos en el archivo .env para pgAdmin.
Registrar el servidor haciendo clic derecho en Servers > Register > Server...
En la pestaña Connection, usar como Host: data-warehouse (el nombre del servicio en Docker) y las credenciales de PostgreSQL del .env