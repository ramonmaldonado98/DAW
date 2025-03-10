# Práctica 2: Creación y Publicación de una Imagen Docker

En esta práctica se detalla el proceso para crear una imagen personalizada de Docker, ejecutarla localmente y publicarla en Docker Hub.

## Paso 1: Mostrar el mensaje "Hello World"
Para verificar que Docker está correctamente instalado, se puede ejecutar el siguiente comando:

```bash
sudo docker run hello-world
```

![Hello World](https://github.com/user-attachments/assets/f2a86546-27fe-4885-9ce3-40cfb4d69a3b)

---

## Paso 2: Mostrar las imágenes disponibles
Para listar las imágenes presentes en el sistema:

```bash
sudo docker images
```

![Listado de Imágenes](https://github.com/user-attachments/assets/c0faef19-ffe1-4283-a2c5-5a933e57bea8)

---

## Paso 3: Mostrar contenedores activos
Para ver los contenedores que se están ejecutando:

```bash
sudo docker ps
```

![Listado de Contenedores](https://github.com/user-attachments/assets/a615829a-2a31-4651-9433-6d1dd791ba71)

---

## Paso 4: Crear el Dockerfile
Crear un nuevo directorio para el proyecto y acceder a él:

```bash
mkdir mi_proyecto
cd mi_proyecto
nano Dockerfile
```

![Creación del Dockerfile](https://github.com/user-attachments/assets/978eeef4-d2bf-48cc-9345-766037b9bb44)

Dentro del archivo `Dockerfile`, incluir la siguiente configuración:

```dockerfile
# Indica la imagen base
FROM ubuntu:latest

# Actualiza paquetes e instala, por ejemplo, curl
RUN apt-get update && apt-get install -y curl

# Mensaje o comando que se ejecutará por defecto
CMD ["echo", "Hola desde mi contenedor!"]
```

![Configuración del Dockerfile](https://github.com/user-attachments/assets/9b2a0e83-df91-49df-90ba-cd5ba2dcc81e)

---

## Paso 5: Construir la imagen
Ejecutar el siguiente comando para crear la imagen:

```bash
docker build -t proyecto .
```

![Construcción del Proyecto](https://github.com/user-attachments/assets/4ff6e9a1-02d8-4f40-bc84-6e28e5594a02)

---

## Paso 6: Ejecutar la imagen
Para ejecutar la imagen creada:

```bash
docker run proyecto
```

![Ejecución de la Imagen](https://github.com/user-attachments/assets/0b43603a-88f9-4058-bdcd-7812c86f5d1f)

---

## Paso 7: Publicar la imagen en Docker Hub
### 1. Crear una cuenta en [hub.docker.com](https://hub.docker.com)

![Registro en Docker Hub](https://github.com/user-attachments/assets/d960e793-8dda-4230-9d63-ae4a1047cac1)

### 2. Crear un repositorio en Docker Hub

![Creación del Repositorio](https://github.com/user-attachments/assets/26811ba2-fd44-48ae-8801-7876d1d676b2)

### 3. Iniciar sesión en Docker Hub desde la terminal

```bash
docker login
```

![Inicio de Sesión](https://github.com/user-attachments/assets/327488d6-6981-4cbc-ad94-02bd7b85ecca)

### 4. Etiquetar la imagen para publicarla

```bash
docker tag proyecto javiersand2/proyecto:latest
```

### 5. Subir la imagen al repositorio

```bash
docker push javiersand2/proyecto:latest
```

![Subida de la Imagen](https://github.com/user-attachments/assets/4f25edd5-8143-4c37-866a-527620bfe8c2)

---

Con estos pasos, habrás creado, ejecutado y publicado exitosamente una imagen Docker personalizada.

