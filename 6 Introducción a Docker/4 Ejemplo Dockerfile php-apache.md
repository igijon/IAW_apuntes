#docker #dockerfile #apache 

# 4. Ejemplo Dockerfile: php-apache

@[José Luis González Sánchez](https://github.com/joseluisgs)         @Inma Gijón Cardos 

# Dockerfile

<aside>
🛠 Un Dockerfile es un archivo de texto plano que contiene una serie de instrucciones necesarias para crear una imagen.

</aside>

- Sintaxis
    
    **FROM:** indica la imagen base sobre la que construir la aplicación dentro del contenedor.
    
    **RUN:** ejecutar comandos en el contenedor: `apt install`, `yum install`...
    
    **ENV:** variables de entorno para nuestro contenedor
    
    **ADD:** copia archivos dentro del contenedor, permite además descargar recursos remotos (URL) o extraer TAR
    
    **COPY:** copia archivos dentro del contenedor
    
    **LABEL: p**ermite indicar información como por ejemplo author
    
    **CMD:** nos permite definir comandos que sólo se ejecutarán cuando el contenedor ya se ha inicializado, por ejemplo comandos Shell con parámetros establecidos.
    
    **ENTRYPOINT: d**efine el comando y los parámetros que se ejecutan primero cuando se ejecuta el contenedor. Todos los comandos pasados en la instrucción `docker run <image>` serán agregados al comando entrypoint.
    
    **VOLUME:** crea el volúmen o punto de montaje dentro del contenedor y es visible desde el host del anfitrión marcado con otro nombre.
    
    **USER:** determina el usuario a utilizar cuando se ejecuta un contenedor y adicionalmente cuando se ejecutan comandos como RUN, CMD, ENTRYPOINT, WORKDIR.
    

[Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

<aside>
👩🏻‍💻 Vamos a crear una primera imagen de apache con php utilizando Dockerfile.

</aside>

Creamos un directorio donde tendremos nuestro proyecto:

```bash
sudo mkdir ejemplo-apache-php
sudo mkdir ejemplo-apache-php/src #creamos el directorio donde tendremos los fuentes que vamos a desplegar
cd ejemplo-apache-php/src
nano index.php
```

<aside>
👩🏻‍💻 Podéis crear el proyecto con cualquier IDE (VSCode, por ejemplo) o añadir un proyecto de php que tengáis para probar.

</aside>

```php
<!-- src/index.php -->
<?php
    phpinfo();
?>
```

Creamos el fichero **Dockerfile**

```docker
#Imagen a usar
FROM php:8.0-apache
# Copiamos todos los fuentes en la ruta de apache
COPY src/ /var/www/html
# Exponemos el puerto 80
EXPOSE 80
LABEL author="José Luis González"
```

Una vez creado y guardado, creamos la imagen con:

```docker
docker build -t miapache-php . 
```

Estamos indicando que genere la imagen miapache-php a partir del directorio actual que es en el que se encuentra el fichero Dockerfile.

Comprobamos que existe

```docker
docker images
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/4%20Ejemplo%20Dockerfile%20php-apache/Untitled.png)

Lanzamos la imagen:

```docker
docker run -dit --name=miapache-php-contenedor -p5555:80 miapache-php
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/4%20Ejemplo%20Dockerfile%20php-apache/Untitled%201.png)

Podemos parar y arrancar mi contenedor (o borrarlo), para ello:

```docker
docker stop miapache-php
docker start miapache-php
```

También puedo agregar contenido a mi carpeta de trabajo y rearmarlo todo, para ello puedo crearme un fichero `run.sh`

```bash
#!/bin/bash
docker rmi -f miapache-php
docker rm -f miapache-php-contenedor
docker build -t miapache-php .
docker run -dit --name=miapache-php-contenedor -p5555:80 miapache-php
```