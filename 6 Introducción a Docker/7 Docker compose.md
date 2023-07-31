# 7. Docker compose

#docker #docker-compose 

@[José Luis González Sánchez](https://github.com/joseluisgs)    @Inma Gijón Cardos

El cliente de Docker es engorroso para crear contenedores, para el resto de objetos y vincularlos entre sí a base de Dockerfiles.

Para automatizar la creación, inicio y parada de un contenedor o conjunto de ellos, Docker proporciona la herramienta **Docker compose.**

**Docker compose** es una herramienta para definir y ejecutar aplicaciones multicontenedor. Con un sólo comando podremos crear e iniciar todos los servicios que necesitamos para nuestra aplicación.

Un `docker-compose.yaml` muy básico tiene este aspecto:

```docker
version: '2'
services:
	hello_world:
		image: ubuntu
		command: [/bin/echo, 'Hola Docker Compose']
```

Vamos a crear el fichero `docker-compose.yaml`para el ejemplo de MariaDB y PHP-Apache.

```docker
version: '3'
services:
  db: 
    image: mariadb:latest
    container_name: mymariadb
    volumes:
      - ./src:/var/lib
      - mariadb_volume:/var/lib/mysql
    environment:
      - TZ='Europe/Rome'
      - MYSQL_ROOT_PASSWORD=secret
      - MYSQL_DATABASE=mariadb_example
      - MYSQL_USER=manager
      - MYSQL_PASSWORD=secret
  php-apache:
    image: myapache_php
    container_name: myapache-php
    ports:
      - "5555:80"
    depends_on: 
      - db
    volumes:
      - ./src:/var/www/html
volumes: 
  mariadb_volume:
```

<aside>
💡 La identación en yaml se produce con espacios, no tabuladores.

</aside>

En el mismo directorio donde tenemos el fichero `docker-compose.yaml`vamos a tener un fichero `Dockerfile` para la generación de la imagen del contenedor de php y apache (tal y como hicimos en el ejemplo anterior)

```docker
#Dockerfile php-apache
#Imagen a usar
FROM php:7.4.4-apache
#Instalamos lo necesario para el acceso a BDD mariadb
RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN a2enmod rewrite
# Copiamos todos los fuentes en la ruta de apache
COPY /src /var/www/html
# Exponemos el puerto 80
EXPOSE 80
LABEL author="Inma Gijón"
```

Nos quedaría por un lado generar la imagen que va a cargar **docker-compose** y por otro lado restaurar la BDD. Para ello podemos tener un fichero `run.sh`

```bash
#!/bin/bash
docker rmi -f myapache_php
docker rm -f myapache_php
docker build -t myapache_php .
docker-compose up -d
docker exec mymariadb bash -c "sleep 5 && mysql -umanager -psecret mariadb_example < /var/lib/example_database.sql"
```

En el directorio src (dentro del mismo directorio) podremos tener el fichero `example_database.sql` e `index.php` para nuestro ejemplo.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/7%20Docker%20compose/Untitled.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/7%20Docker%20compose/Untitled%201.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/7%20Docker%20compose/Untitled%202.png)