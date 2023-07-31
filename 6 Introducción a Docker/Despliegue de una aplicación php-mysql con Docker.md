#docker 

# Despliegue de una aplicación php-mysql con Docker compose

Tienes los fuentes disponibles aquí:

[ejemplo_docker_compose_completo.zip](https://drive.google.com/file/d/1Tzk4YUdYiGNP93MdvD81a6DIU7adJfj7/view?usp=sharing)

# docker-compose.yaml

```docker
version: '3'
services:
  db: 
    image: mariadb:latest
    container_name: mymariadb
    hostname: mymariadb
    networks:
      - inma-network
    volumes:
      - ./src:/var/lib
      - mariadb_volume:/var/lib/mysql
    ports:
      - "3306:3306"
    environment:
      - TZ='Europe/Rome'
      - MYSQL_ROOT_PASSWORD=secret
      - MYSQL_DATABASE=mariadb_example
      - MYSQL_USER=manager
      - MYSQL_PASSWORD=secret
    
  php-apache:
    build:
      context: myapache_php
    image: myapache_php
    container_name: myapache-php
    hostname: php_apache
    networks:
      - inma-network
    ports:
      - "5555:80"
    depends_on: 
      - db
    volumes:
      - ./src:/var/www/html

  initializer:
    build:
      context: myapache_php
    image: myapache_php
    container_name: db-initializer
    hostname: initializer
    environment:
      - MYSQL_HOST=mymariadb
      - MYSQL_DATABASE=mariadb_example
      - MYSQL_USER=manager
      - MYSQL_PASSWORD=secret
      - MYSQL_SCRIPT=example_database.sql
    networks:
      - inma-network
    depends_on: 
      - db
 #  command: [ "tail", "-f" ]  
    command: [ "bash", "./dbinitializer.sh" ]
    volumes:
      - ./src:/var/www/html

volumes: 
  mariadb_volume: 

networks:
  inma-network:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 173.50.0.0/24
```

# myapache_php/Dockerfile

```docker
#Dockerfile php-apache
#Imagen a usar
FROM php:7.4.4-apache
#Instalamos lo necesario para el acceso a BDD mariadb
RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN a2enmod rewrite
# esto no es necesario aquí. para hacerlo fino crearia otra imagen con alpine + cliente
RUN apt update && apt install default-mysql-client -y
# Copiamos todos los fuentes en la ruta de apache
#COPY /src /var/www/html
# Exponemos el puerto 80
EXPOSE 80
LABEL author="Inma Gijón"
```

# src/dbinicializer.sh

```bash
#!/bin/bash
set -x
mysql -u"${MYSQL_USER}" -p"${MYSQL_PASSWORD}" -h"${MYSQL_HOST}" "${MYSQL_DATABASE}" < "${MYSQL_SCRIPT}"
```

# Levantando...

```docker
docker-compose up db
docker-compose up initializer
docker-compose up php-apache
```