# Backend Despachos - API REST

API REST desarrollada con Spring Boot para la gestión de órdenes de despacho del sistema ITPCargo.

## Tecnologías

- Java 17
- Spring Boot 3.4.4
- MySQL 8.0
- Docker
- Maven

## Endpoints

| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | /api/v1/despachos | Obtener todos los despachos |
| GET | /api/v1/despachos/{id} | Obtener despacho por ID |
| POST | /api/v1/despachos | Crear nuevo despacho |
| PUT | /api/v1/despachos/{id} | Actualizar despacho |
| DELETE | /api/v1/despachos/{id} | Eliminar despacho |

Documentación completa disponible en `/swagger-ui.html` una vez iniciado el servicio.

## Variables de entorno

| Variable | Descripción |
|----------|-------------|
| DB_ENDPOINT | Host de la base de datos |
| DB_PORT | Puerto de la base de datos |
| DB_NAME | Nombre de la base de datos |
| DB_USERNAME | Usuario de la base de datos |
| DB_PASSWORD | Contraseña de la base de datos |

## Correr localmente con Docker

1. Clonar el repositorio
2. Crear archivo `.env` basado en las variables de entorno descritas arriba
3. Ejecutar:

```bash
docker-compose up -d
```

El servicio estará disponible en `http://localhost:8081`

## Pipeline CI/CD

El pipeline se activa automáticamente al hacer push sobre la rama `deploy`.

Pasos del pipeline:
1. Construcción de la imagen Docker (multi-stage build)
2. Publicación de la imagen en Docker Hub
3. Despliegue automático en la instancia EC2

### Secrets requeridos en GitHub

| Secret | Descripción |
|--------|-------------|
| DOCKERHUB_USERNAME | Usuario de Docker Hub |
| DOCKERHUB_TOKEN | Token de acceso Docker Hub |
| EC2_BACKEND_HOST | IP pública del servidor EC2 |
| EC2_USER | Usuario SSH del EC2 |
| EC2_SSH_KEY | Clave privada SSH |
| DB_ENDPOINT | Host de la base de datos |
| DB_PORT | Puerto de la base de datos |
| DB_NAME_DESPACHOS | Nombre de la base de datos |
| DB_USERNAME | Usuario de la base de datos |
| DB_PASSWORD | Contraseña de la base de datos |

## Dockerfile

El Dockerfile utiliza multi-stage build:
- **Stage 1 (builder):** Compila el proyecto con Maven y genera el archivo `.jar`
- **Stage 2 (runtime):** Ejecuta la aplicación usando solo el JRE (más liviano), con usuario sin privilegios root

## Persistencia de datos

Los datos se persisten mediante un volumen Docker llamado `mysql_despachos_data` definido en el `docker-compose.yml`. Esto garantiza que los datos no se pierdan al reiniciar los contenedores.
