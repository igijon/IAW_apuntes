#docker #mariadb


# 5. Persistencia. Volúmenes. MariaDB. Importar BDD.

@[José Luis González Sánchez](https://github.com/joseluisgs)    @Inma Gijón Cardos

Si queremos almacenar datos (una web, una BDD...) dentro de un contenedor necesitamos una manera de almacenarlos sin perderlos.

**Docker ofrece tres maneras:**

- A través de volúmenes que son objetos de Docker como las imágenes y los contenedores.
- Montando un directorio de la máquina anfitrión dentro del contenedor (enlazando directorios).
- Almacenando en la memoria del sistema (aunque también se perderían al reiniciar el servidor).

Lo normal, por ejemplo, para guardar los datos de una BDD usaremos volúmenes, pero para guardar el código de una aplicación o de una página web montaremos un directorio. La razón para esto es que tanto nuestro entorno de desarrollo como el contenedor tengan acceso a los archivos del código fuente. Los volúmenes, al contrario que los directorios montados, no deben accederse desde la máquina anfitrión.

## Enlazando directorios

Por ejemplo, sobre el ejemplo anterior:

```bash
docker run -dit --name=miapache-php -p5555:80 --mount type=bind,source="$PWD/src",target=/var/www/html miapache-php
docker run -dit --name=miapache-php -p5555:80 --mount type=bind,source="%cd%/src",target=/var/www/html miapache-php #Windows
```

Si accedemos:

```bash
docker exec -it miapache-php /bin/bash
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/5%20Persistencia%20Volúmenes%20MariaDB%20Importar%20BDD/Untitled.png)

Podemos ver que se encuentra el contenido de `$PWD/src`

# Volúmenes

En el ejemplo que vimos aquí, creamos un docker apache con un volumen automático (no elegimos su nombre, se creó sobre la marcha) usando la opción `-v` y enlazado a un directorio.

[3. Primer ejemplo Docker: Apache](https://pinnate-damselfly-ade.notion.site/3-Primer-ejemplo-Docker-Apache-45cfefb38ecc4dcbba86555d35f3a133)

<aside>
💡 Los volúmenes son independientes de los contenedores, pero Docker tiene en cuenta qué volúmenes están siendo utilizados por un contenedor y no permite borrar el volúmen si hay contenedores que lo están usando, aunque estén detenidos.

</aside>

```bash
docker volume ls #lista los volúmenes
docker rm volume-name
```

Para desplegar nuestros proyectos, necesitamos tener la BDD así que vamos a realizar algunos ejemplos sobre esto.

```bash
docker run -d --name=mymariadb --mount source=mariadb,target=/var/lib/mysql -eMYSQL_ROOT_PASSWORD=secret -eMYSQL_DATABASE=mariadb_example -eMYSQL_USER=manager -eMYSQL_PASSWORD=secret mariadb:latest
```

Esto levantará una instancia de **mariadb,** creando un volumen y con las variables de entorno que le estamos indicando.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/5%20Persistencia%20Volúmenes%20MariaDB%20Importar%20BDD/Untitled%201.png)

En esta ocasión, no hemos utilizado `-p` para publicar puertos.

Podemos ver que nuestro contenedor está usando el puerto `3306/tcp`pero no está linkado a la máquina anfitrión. No tenemos forma de acceder a la BDD directamente. Nuestra intención es que sólo el contenedor de **apache-php** pueda acceder más adelante.

Los parámetros `-e` nos permiten configurar nuestra BDD.

Por último, el parámetro `—-mount`nos permite enlazar el volumen que creamos en el paso anterior con el directorio `/var/lib/mysql` del contenedor. Este directorio es dónde se guardan los datos de MariaDB. Si borramos el contenedor o lo actualizamos a una nueva versión, no perderemos los datos porque están en el volumen. **Sólo se borrarán si se borra explícitamente el volumen.**

Si entramos en el contenedor:

```bash
docker exec -it mymariadb /bin/bash
```

Puedo acceder a la consola de `mysql` con el usuario configurado y puedo ver que la BDD que hemos indicado en la configuración:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/5%20Persistencia%20Volúmenes%20MariaDB%20Importar%20BDD/Untitled%202.png)

Si quiero restaurar la BDD que tengo en el anfitrión en local con el fichero: **example_database.sql** puedo enlazar un directorio también de este modo:

```bash
docker run -d --name=mymariadb --mount type=bind,source="$PWD",target="/var" --mount source=mariadb,target=/var/lib/mysql -eMYSQL_ROOT_PASSWORD=secret -eMYSQL_DATABASE=mariadb_example -eMYSQL_USER=manager -eMYSQL_PASSWORD=secret mariadb:latest

docker run -d --name=mymariadb --mount type=bind,source="./mount",target="/var" --mount source=mariadb,target=/var/lib/mysql -eMYSQL_ROOT_PASSWORD=secret -eMYSQL_DATABASE=mariadb_example -eMYSQL_USER=manager -eMYSQL_PASSWORD=secret mariadb:latest #Para Windows
```

Puedo entrar en el contenedor y restaurar la BDD (más adelante lo haremos de otro modo):

```bash
docker exec -it mymariadb /bin/bash
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/5%20Persistencia%20Volúmenes%20MariaDB%20Importar%20BDD/Untitled%203.png)

Puedo restaurar la BDD:

[example_database.sql](https://drive.google.com/file/d/19dX74vQGZD_wTput1hlnRgR0pfMoQLHr/view?usp=sharing)

```bash
mysql -u manager -p mariadb_example < example_database.sql
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/5%20Persistencia%20Volúmenes%20MariaDB%20Importar%20BDD/Untitled%204.png)

Comprobamos que se ha importado:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/5%20Persistencia%20Volúmenes%20MariaDB%20Importar%20BDD/Untitled%205.png)