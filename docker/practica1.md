
# Práctica 1: Instalación de Docker

Este documento detalla el procedimiento para instalar Docker en un sistema operativo basado en Ubuntu, asegurando que no haya conflictos con paquetes preexistentes.

## Paso 1: Limpieza del sistema
Antes de proceder con la instalación, es recomendable eliminar cualquier paquete que pueda generar conflictos con Docker. Para ello, ejecute el siguiente comando:

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

![Eliminación de paquetes](https://github.com/user-attachments/assets/5789063c-66b2-47f7-9dba-c2a97f4db4c8)

---

## Paso 2: Preparar el entorno para Docker
Actualizar los paquetes e instalar las dependencias necesarias:

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
```

![Actualización e instalación de dependencias](https://github.com/user-attachments/assets/f6a672c5-a938-445f-9121-6964cf578d9c)

---

## Paso 3: Configuración del repositorio Docker
Crear el directorio de claves para APT:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

Descargar la clave GPG oficial de Docker:

```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```

Establecer los permisos adecuados para la clave:

```bash
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Añadir el repositorio oficial de Docker:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

![Añadiendo repositorio](https://github.com/user-attachments/assets/ead15c89-5ad4-451b-9d3b-d8022823eb85)

---

## Paso 4: Instalación de Docker
Instalar los paquetes principales de Docker:

```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

![Instalación de Docker](https://github.com/user-attachments/assets/29622c47-6993-43ea-ad9b-8c3a06614e55)

---

## Paso 5: Verificación de la instalación
Para comprobar que Docker se ha instalado correctamente, ejecute el siguiente comando:

```bash
sudo docker run hello-world
```

Si la instalación fue exitosa, se mostrará un mensaje de confirmación.

![Prueba de Docker](https://github.com/user-attachments/assets/8938d06f-775e-4f9e-841a-b2921fa49130)

---

Con estos pasos, Docker estará correctamente instalado y listo para su uso.

