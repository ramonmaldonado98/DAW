# Práctica 3: Gestión de Imágenes y Contenedores Docker

En esta práctica se detalla el proceso para descargar imágenes Docker, ejecutar contenedores y gestionar su ciclo de vida.

---

## Paso 1: Descargar la imagen de Ubuntu
Para descargar la imagen oficial de Ubuntu, ejecute el siguiente comando:

```bash
docker pull ubuntu
```

![Descarga de imagen Ubuntu](https://github.com/user-attachments/assets/0d3c83b3-3fee-4279-80d1-da1dd79198a6)

---

## Paso 2: Ejecutar el contenedor "Hello World"
Ejecute el siguiente comando para probar la imagen de "Hello World":

```bash
docker run hello-world
```

![Ejecución de Hello World](https://github.com/user-attachments/assets/753d800d-a243-437b-8848-f27ded1a2adf)

---

## Paso 3: Descargar la imagen de Nginx
Para descargar la imagen oficial de Nginx, utilice el siguiente comando:

```bash
docker pull nginx
```

![Descarga de imagen Nginx](https://github.com/user-attachments/assets/e8e59794-449d-428b-9f51-15bef4737dac)

---

## Paso 4: Listar las imágenes disponibles
Para mostrar todas las imágenes descargadas en el sistema:

```bash
docker images
```

![Listado de imágenes](https://github.com/user-attachments/assets/ff58ec24-4c57-4274-a84e-e75fbd85c0dd)

---

## Paso 5: Ejecutar un contenedor con nombre personalizado
Para ejecutar el contenedor "Hello World" y asignarle un nombre:

```bash
docker run --name myhello1 hello-world
```

![Ejecución de contenedor con nombre](https://github.com/user-attachments/assets/80f4f9ac-30fe-4756-8b6a-ac016a25c36c)

---

## Paso 6: Mostrar los contenedores activos
Para ver los contenedores que se están ejecutando:

```bash
docker ps
```

![Listado de contenedores activos](https://github.com/user-attachments/assets/92fd50f2-cf4b-46ea-a951-99e571a6ade8)

---

## Paso 7: Detener los contenedores
Para detener uno o varios contenedores, utilice los siguientes comandos:

```bash
docker stop myhello1
```

```bash
docker stop myhello2
```

```bash
docker stop myhello3
```

---

## Paso 8: Eliminar los contenedores
Para eliminar contenedores específicos:

```bash
docker rm myhello1
```

```bash
docker rm myhello2
```

```bash
docker rm myhello3
```

---

## Paso 9: Eliminar todos los contenedores de forma masiva
Si desea eliminar todos los contenedores de forma automática:

```bash
docker rm -f $(docker ps -aq)
```

![Eliminación masiva de contenedores](https://github.com/user-attachments/assets/2eeea07f-f0e1-492e-a93c-7326dc46154a)

---

Con estos pasos, habrás descargado imágenes, ejecutado contenedores y aprendido a gestionarlos de forma eficiente.

