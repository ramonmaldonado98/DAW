# Configuración de Servicios con Docker Compose

## Ejemplo 1: Guestbook

A continuación, se muestra un archivo `docker-compose.yml` para desplegar un servicio de Guestbook con Redis.

```yaml
version: '3.1'
services:
  app:
    container_name: guestbook
    image: iesgn/guestbook
    restart: always
    environment:
      REDIS_SERVER: redis
    ports:
      - 8080:5000
  db:
    container_name: redis
    image: redis
    restart: always
    command: redis-server --appendonly yes
    volumes:
      - redis:/data
volumes:
  redis:
```

### Creación del Entorno

Para crear el entorno, ejecutamos el archivo `docker-compose.yml`:

![Creación del entorno](https://github.com/user-attachments/assets/0df73d8c-0c54-4c3e-ae69-57eca36b5ec3)

### Acceso a la Aplicación

Una vez desplegado, podemos acceder a la aplicación en `localhost`:

![Acceso a localhost](https://github.com/user-attachments/assets/7a520e66-82b4-4531-a710-fedb857c61ea)

---

## Ejemplo 2: Página de Temperaturas

A continuación, se configura un entorno Docker para una aplicación de monitoreo de temperaturas con arquitectura frontend-backend.

### Archivo `docker-compose.yml`

```yaml
version: '3.1'
services:
  frontend:
    container_name: temperaturas-frontend
    image: iesgn/temperaturas_frontend
    restart: always
    ports:
      - 8081:3000
    environment:
      TEMP_SERVER: temperaturas-backend:5000
    depends_on:
      - backend
  backend:
    container_name: temperaturas-backend
    image: iesgn/temperaturas_backend
    restart: always
```

### Implementación del Entorno

Ejecutamos el archivo `docker-compose.yml` para desplegar los servicios:

![Implementación del entorno](https://github.com/user-attachments/assets/5a139261-1be8-456c-a5fa-31d7959f45ac)
