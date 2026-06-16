# Backend Despachos - Innovatech Chile

API REST desarrollada con Spring Boot para la gestión de órdenes de despacho del sistema Innovatech Chile. Desplegada en AWS ECS con Fargate y conectada a Amazon RDS MySQL.

## Tecnologías

- Java 17
- Spring Boot 3.4
- MySQL 8.0 (Amazon RDS)
- Docker
- Maven

## Endpoints

| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/v1/despachos` | Listar órdenes de despacho |
| POST | `/api/v1/despachos` | Crear orden de despacho |
| PUT | `/api/v1/despachos/{id}` | Actualizar orden de despacho |

## Variables de entorno

| Variable | Descripción |
|----------|-------------|
| `DB_ENDPOINT` | Endpoint de la base de datos RDS |
| `DB_PORT` | Puerto de la base de datos (3306) |
| `DB_NAME` | Nombre de la base de datos |
| `DB_USERNAME` | Usuario de la base de datos |
| `DB_PASSWORD` | Contraseña de la base de datos |
| `SPRING_DATASOURCE_URL` | URL completa de conexión JDBC |

## Pipeline CI/CD

Cada push a la rama `deploy` activa el workflow de GitHub Actions que:
1. Construye la imagen Docker
2. Hace push a Amazon ECR
3. Fuerza un nuevo despliegue en ECS

## Cómo correr localmente

Crear un archivo `.env` con las variables de entorno y ejecutar:

```bash
./mvnw spring-boot:run
```
