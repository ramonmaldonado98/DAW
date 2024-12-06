# Configuración de un Servidor Web Interno en Ubuntu

Este proyecto detalla los pasos necesarios para instalar y configurar un servidor web interno utilizando Apache para soportar WordPress y aplicaciones Python, además de un servidor Nginx para gestionar PHP y phpMyAdmin.

---

## 1. Instalación del Servidor Web Apache

### Actualizar los repositorios e instalar Apache:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/1/1.png)

sudo apt update
sudo apt install apache2 -y


### Configurar el archivo /etc/hosts:
Edita el archivo:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/1/2.png)

sudo nano /etc/hosts

Añade las siguientes líneas:

127.0.0.1 centro.intranet
127.0.0.1 departamentos.centro.intranet


### Configurar Virtual Hosts:
#### Para centro.intranet:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/1/3.png)

sudo nano /etc/apache2/sites-available/centro.intranet.conf

Contenido:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/1/4.png)

<VirtualHost *:80>
    ServerName centro.intranet
    DocumentRoot /var/www/centro.intranet
</VirtualHost>


#### Para departamentos.centro.intranet:

sudo nano /etc/apache2/sites-available/departamentos.centro.intranet.conf

Contenido:

<VirtualHost *:80>
    ServerName departamentos.centro.intranet
    DocumentRoot /var/www/departamentos.centro.intranet
</VirtualHost>


### Activar sitios y reiniciar Apache:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/1/5.png)

sudo mkdir -p /var/www/centro.intranet /var/www/departamentos.centro.intranet
sudo a2ensite centro.intranet.conf
sudo a2ensite departamentos.centro.intranet.conf
sudo systemctl reload apache2


---

## 2. Activar módulos necesarios para PHP y MySQL

### Instalar PHP, MySQL y módulos necesarios:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/2/1.png)

sudo apt install php libapache2-mod-php php-mysql mysql-server -y


### Activar módulos de Apache:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/2/2.png)

sudo a2enmod php
sudo systemctl reload apache2


### Verificar PHP:
Crea un archivo de prueba:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/2/3.png)

echo "<?php phpinfo(); ?>" | sudo tee /var/www/centro.intranet/info.php

Accede a `http://centro.intranet/info.php` desde tu navegador.

---

## 3. Instalar y Configurar WordPress

### Descargar e instalar WordPress:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/3/1.png)

wget https://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
sudo mv wordpress/* /var/www/centro.intranet/


### Configurar permisos:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/3/2.png)

sudo chown -R www-data:www-data /var/www/centro.intranet
sudo chmod -R 755 /var/www/centro.intranet


### Configurar la base de datos:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/3/3.png)

sudo mysql

En el shell de MySQL:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/3/4.png)

CREATE DATABASE wordpress;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;


Completa la configuración accediendo a http://centro.intranet en tu navegador.

---

## 4. Activar el módulo WSGI para Python

### Instalar y activar el módulo:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/4/1.png)

sudo apt install libapache2-mod-wsgi-py3 -y
sudo a2enmod wsgi
sudo systemctl reload apache2


---

## 5. Desplegar una Aplicación Python

### Crear la aplicación Python:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/5/1.png)

sudo nano /var/www/departamentos.centro.intranet/app.wsgi

Contenido:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/5/2.png)

def application(environ, start_response):
    status = '200 OK'
    output = b'Hello, Python Application!'
    response_headers = [('Content-Type', 'text/plain'),
                        ('Content-Length', str(len(output)))]
    start_response(status, response_headers)
    return [output]


### Configurar el Virtual Host para Python:
Edita /etc/apache2/sites-available/departamentos.centro.intranet.conf:

<VirtualHost *:80>
    ServerName departamentos.centro.intranet
    DocumentRoot /var/www/departamentos.centro.intranet
    WSGIScriptAlias / /var/www/departamentos.centro.intranet/app.wsgi
</VirtualHost>


Reinicia Apache:

sudo systemctl reload apache2


---

## 6. Proteger la Aplicación Python con Autenticación

### Crear un archivo de contraseñas:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/6/1.png)

sudo apt install apache2-utils
sudo htpasswd -c /etc/apache2/.htpasswd user1


### Configurar autenticación en el Virtual Host:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/6/2.png)

Edita /etc/apache2/sites-available/departamentos.centro.intranet.conf:


![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/6/3.png)

<Directory /var/www/departamentos.centro.intranet>
    AuthType Basic
    AuthName "Restricted Access"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>


Reinicia Apache:

sudo systemctl reload apache2


---

## 7. Instalar y Configurar AWStats

### Instalar AWStats:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/7/1.png)

sudo apt install awstats -y


### Configurar AWStats:
Edita el archivo de configuración:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/7/2.png)

sudo nano /etc/awstats/awstats.localhost.conf

Modifica SiteDomain a:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/7/3.png)

SiteDomain="centro.intranet"


Generar estadísticas manualmente:

sudo awstats --update -config=localhost


---

## 8. Configurar un Segundo Servidor (Nginx)

### Instalar Nginx y PHP-FPM:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/8/1.png)

sudo apt install nginx php-fpm -y


### Configurar el Virtual Host en Nginx:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/8/2.png)

Edita /etc/nginx/sites-available/servidor2.centro.intranet:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/8/3.png)

server {
    listen 8080;
    server_name servidor2.centro.intranet;
    root /var/www/servidor2.centro.intranet;

    index index.php index.html;

    location ~ \\.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    }
}


Habilita el sitio y reinicia Nginx:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/8/4.png)

sudo ln -s /etc/nginx/sites-available/servidor2.centro.intranet /etc/nginx/sites-enabled/
sudo mkdir -p /var/www/servidor2.centro.intranet
sudo systemctl restart nginx


### Instalar phpMyAdmin:

![](https://github.com/ramonmaldonado98/DAW/blob/main/Práctica1trimestre/Capturas/8/5.png)

sudo apt install phpmyadmin -y
