#docker #apache 

# 3. Primer ejemplo Docker: Apache

@[José Luis González Sánchez](https://github.com/joseluisgs)         @Inma Gijón Cardos 

<aside>
💡 Creamos un contenedor a partir de la imagen bitnami/apache y con -P Docker asigna de forma aleatoria un puerto de la máquina virtual al puerto asignado a Apache en el contenedor. La imagen bitnami/apache asigna a Apache el puerto 8080 del contenedor para conexiones http y el puerto 8443 para conexiones https.

</aside>

```bash
docker run -d -P --name=apache-1 bitnami/apache
```

```bash
docker ps -a #consultamos el puerto
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/3%20Primer%20ejemplo%20Docker%20Apache/Untitled.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/3%20Primer%20ejemplo%20Docker%20Apache/Untitled%201.png)

<aside>
💡 Vamos a modificar el contenido de la página de inicio de Apache pero **habitualmente no lo haremos así**, porque **los contenedores Docker están pensados como objetos de “usar y tirar”, es decir, para ser creados, destruidos tantas veces como se quiera.**

</aside>

<aside>
💡 Creamos el contenedor a partir de la imagen httpd

</aside>

```bash
docker run -d -P --name=apache-SEPECAM httpd
docker ps -a
```

Creamos una nueva página html: `index.html` con el contenido que queramos para la prueba.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/3%20Primer%20ejemplo%20Docker%20Apache/Untitled%202.png)

<aside>
💡 Vamos a entrar en la shell del contenedor para averiguar la ubicación de la página inicial

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/3%20Primer%20ejemplo%20Docker%20Apache/Untitled%203.png)

</aside>

```bash
sudo docker exec -it apache-SEPECAM /bin/bash
exit
```

<aside>
💡 Vemos que está en `/usr/local/apache2/htdocs`

</aside>

```bash
docker cp index.html apache-SEPECAM:/usr/local/apache2/htdocs
docker ps #vemos el puerto
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/3%20Primer%20ejemplo%20Docker%20Apache/Untitled%204.png)

Desplegada!

# Sin copiar ficheros

```bash
docker run -dit --name=apache-SEPECAM2 -p5555:80 -v"$PWD":/usr/local/apache2/htdocs httpd #Sistemas Unix
docker run -dit --name=apache-SEPECAM2 -p5555:80 -v"%cd%":/usr/local/apache2/htdocs httpd #Para windows
```

<aside>
💡 El contenedor tendrá asociado el nombre **apache-SEPECAM2.**

</aside>

<aside>
💡 Se ha mapeado el puerto 80 del contenedor sobre el 5555 de la máquina real.

</aside>

<aside>
💡 Se ha mapeado la ruta de nuestro equipo donde está el fichero `index.html` con la ruta `/usr/local/apache2/htdocs` del contenedor que es donde Apache va a cargar la web que alojemos. En el directorio actual de mi máquina tengo el sitio que quiero cargar.

</aside>

Los volúmenes son independientes de los contenedores, pero Docker tiene en cuenta qué volúmenes están siendo utilizados por un contenedor.

<aside>
💡 con `it` dejamos que tenga acceso a la consola por defecto.

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/3%20Primer%20ejemplo%20Docker%20Apache/Untitled%205.png)

```bash
docker exec -it apache-SEPECAM2 /bin/bash
```

Podemos ver que tenemos todo mapeado:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/3%20Primer%20ejemplo%20Docker%20Apache/Untitled%206.png)