# Guía de Creación de Imágenes y Contenedores con Docker

## Ejemplo 1: Servidor Apache en Debian

A continuación, se muestra el proceso para crear y ejecutar un contenedor Docker con Apache basado en Debian.

### Acceso al Directorio Docker

Nos ubicamos en el directorio de trabajo:

```sh
$ ls
Dockerfile  public_html
```

### Definición del Dockerfile

Se usa una imagen base de Debian y se instala Apache:

```dockerfile
# syntax=docker/dockerfile:1
FROM debian:stable-slim
RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /var/www/html/
COPY public_html .
EXPOSE 80
CMD apache2ctl -D FOREGROUND
```

### Construcción de la Imagen

Ejecutamos el siguiente comando para construir la imagen:

```sh
$ docker build -t javiersand2/ejemplo1:v1 .
```

### Verificación de la Imagen

Comprobamos que la imagen se haya creado correctamente:

```sh
$ docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
javiersand2/ejemplo1     v1                  8c3275799063        1 minute ago      226MB
```

### Creación y Ejecución del Contenedor

```sh
$ docker run -d -p 80:80 --name ejemplo1 josedom24/ejemplo1:v1
```

### Acceso a la Aplicación

Accedemos al servidor desde el navegador:

![Acceso al servidor](https://github.com/user-attachments/assets/12643491-9ef1-4ecd-a50b-ff8bdbc46e70)

---

## Ejemplo 2: Servidor Apache con PHP

A continuación, se configura un contenedor Docker con Apache y PHP.

### Definición del Dockerfile

Se usa una imagen base con PHP 7.4 y Apache:

```dockerfile
# syntax=docker/dockerfile:1
FROM php:7.4-apache
COPY app /var/www/html/
EXPOSE 80
```

### Construcción y Ejecución del Contenedor

```sh
$ docker build -t josedom24/ejemplo2:v2 .
$ docker run -d -p 80:80 --name ejemplo2 josedom24/ejemplo2:v2
```

### Acceso a la Página `info.php`

![Acceso a info.php](https://github.com/user-attachments/assets/056b907b-d516-4a59-a7ee-a08d4d698e43)

---

## Ejemplo 3: Aplicación en Python

A continuación, se configura un contenedor Docker con Python y dependencias instaladas con `pip`.

### Definición del Dockerfile

```dockerfile
# syntax=docker/dockerfile:1
FROM debian:12
RUN apt-get update && apt-get install -y python3-pip  && apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /usr/share/app
COPY app .
RUN pip3 install --no-cache-dir --break-system-packages -r requirements.txt
EXPOSE 3000
CMD python3 app.py
```

### Construcción y Verificación de la Imagen

```sh
$ docker build -t josedom24/ejemplo3:v1 .
$ docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
ramonmaldonado/ejemplo1     v1                  8c3275799063        1 minute ago      226MB
```

### Acceso a la Aplicación

Accedemos desde el navegador:

![Acceso a la aplicación](https://github.com/user-attachments/assets/b975fd7b-1549-47ec-a76a-23744f12fa48)
