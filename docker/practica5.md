# Ejemplos de Docker Compose

## Ejemplo 1: Guestbook con Redis

### Archivo `docker-compose.yml`
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

### Crear el escenario
![image](https://github.com/user-attachments/assets/0df73d8c-0c54-4c3e-ae69-57eca36b5ec3)

### Entrar en el localhost
![image](https://github.com/user-attachments/assets/7a520e66-82b4-4531-a710-fedb857c61ea)

---

## Ejemplo 2: Página de Temperaturas

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

### Crear el escenario
![image](https://github.com/user-attachments/assets/5a139261-1be8-456c-a5fa-31d7959f45ac)

