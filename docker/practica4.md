# Práctica 4: Redes y Contenedores en Docker

En esta práctica se detallan ejemplos de creación de redes y despliegue de contenedores utilizando Docker.

---

## Ejemplo 1: Red y contenedores para Guestbook

### Paso 1: Crear la red

```bash
docker network create red_guestbook
```

![Creación de red](https://github.com/user-attachments/assets/8eeec12d-12e8-46bf-a7fd-3d4fff81e63c)

### Paso 2: Ejecutar los contenedores

**Contenedor Redis**
```bash
docker run -d --name redis --network red_guestbook -v /opt/redis:/data redis redis-server --appendonly yes
```

![Contenedor Redis](https://github.com/user-attachments/assets/6a28973e-b8a3-4641-9f18-620bffd9ddfa)

**Contenedor Guestbook**
```bash
docker run -d -p 80:5000 --name guestbook --network red_guestbook iesgn/guestbook
```

![Contenedor Guestbook](https://github.com/user-attachments/assets/8b5755b0-9bee-45de-913e-6c9c6ea78ab5)

### Paso 3: Visualización de la aplicación

![Visualización de la aplicación](https://github.com/user-attachments/assets/e0688065-8df9-4607-b818-85f9912e8ba7)

---

## Ejemplo 2: Red y contenedores para Temperaturas

### Paso 1: Crear la red

```bash
docker network create red_temperaturas
```

![Creación de red](https://github.com/user-attachments/assets/3f5bd323-2fa5-4cf4-b42b-d217eb7fe822)

### Paso 2: Ejecutar los contenedores

**Contenedor Backend**
```bash
docker run -d --name temperaturas-backend --network red_temperaturas iesgn/temperaturas_backend
```

![Contenedor Backend](https://github.com/user-attachments/assets/d2fc4706-0e58-4434-b186-8090b342ed90)

**Contenedor Frontend**
```bash
docker run -d -p 80:3000 --name temperaturas-frontend --network red_temperaturas iesgn/temperaturas_frontend
```

![Contenedor Frontend](https://github.com/user-attachments/assets/eaac53b1-6304-4eda-9a4f-48cc157007e9)

---

## Ejemplo 3: Red y contenedores para WordPress

### Paso 1: Crear la red

```bash
docker network create red_wp
```

![Creación de red](https://github.com/user-attachments/assets/2b1d95d5-2ac3-4524-8342-eaa98ef1f075)

### Paso 2: Crear los contenedores

**Contenedor MySQL**
```bash
docker run -d --name servidor_mysql \
                --network red_wp \
                -v /opt/mysql_wp:/var/lib/mysql \
                -e MYSQL_DATABASE=bd_wp \
                -e MYSQL_USER=user_wp \
                -e MYSQL_PASSWORD=asdasd \
                -e MYSQL_ROOT_PASSWORD=asdasd \
                mariadb
```

![Contenedor MySQL](https://github.com/user-attachments/assets/81455a17-ddcc-4b16-a379-182b74f27ec4)

**Contenedor WordPress**
```bash
docker run -d --name servidor_wp \
                --network red_wp \
                -v /opt/wordpress:/var/www/html/wp-content \
                -e WORDPRESS_DB_HOST=servidor_mysql \
                -e WORDPRESS_DB_USER=user_wp \
                -e WORDPRESS_DB_PASSWORD=asdasd \
                -e WORDPRESS_DB_NAME=bd_wp \
                -p 80:80 \
                wordpress
```

![Contenedor WordPress](https://github.com/user-attachments/assets/2e14bc6a-67bb-4a11-9322-ddc4bb11b335)

### Paso 3: Mostrar los contenedores activos

```bash
docker ps
```

![Listado de contenedores](https://github.com/user-attachments/assets/9038d7ae-e21d-4db7-9d6b-4a1fb02455a7)

### Paso 4: Abrir WordPress en el navegador

![Apertura de WordPress](https://github.com/user-attachments/assets/5dd1041d-cb5e-4f6c-9d80-c9c8dbaaf1ab)

---

Con estos pasos, habrás configurado redes y desplegado contenedores en Docker para diversos proyectos.

