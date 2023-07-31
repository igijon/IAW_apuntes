
#docker 

# 2. Instalación de Docker y “hello world”

@[José Luis González Sánchez](https://github.com/joseluisgs)         @Inma Gijón Cardos 

[Home - Docker](https://www.docker.com/)

# Descarga Docker Desktop para tu SO

[Developers - Docker](https://www.docker.com/get-started/)

Seguir las indicaciones de la web para su instalación.

# Hello world

```bash
sudo docker run hello-world
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/2%20Instalación%20de%20Docker%20y%20“hello%20world”/Untitled.png)

# Primeros comandos

Para ver los contenedores creados y detenidos...

```bash
docker ps -a 
docker container ls -a #alternativa
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/2%20Instalación%20de%20Docker%20y%20“hello%20world”/Untitled%201.png)

Imágenes disponibles

```bash
docker image ls
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/2%20Instalación%20de%20Docker%20y%20“hello%20world”/Untitled%202.png)

<aside>
💡 Docker crea los contenedores a partir de imágenes locales (ya descargadas), pero si al crear el contenedor, no se dispone de la imagen local, Docker descarga la imagen de su repositorio.

</aside>

```bash
docker run IMAGEN #Si usamos la opción -d se arranca en segundo plano
docker run hello-world #El nombre de la imagen es hello-world
```

<aside>
💡 Cada contenedor tiene un ID y un nombre distinto. Docker los “bautiza” con un nombre compuesto.

</aside>

<aside>
💡 Podemos crear tantos contenedores como queramos a partir de una imagen.

</aside>

```bash
#Borrar un contenedor
docker rm exciting_keldysh
docker ps -a
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/2%20Instalación%20de%20Docker%20y%20“hello%20world”/Untitled%203.png)

```bash
#listar las imágenes
docker images 
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/2%20Instalación%20de%20Docker%20y%20“hello%20world”/Untitled%204.png)

```bash
docker image rm hello-world
```

Podemos crear un contenedor con un nombre

```bash
docker run -d --name=hello-1 hello-world
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/2%20Instalación%20de%20Docker%20y%20“hello%20world”/Untitled%205.png)

En Docker Desktop podemos de forma visual ver la información y gestionar contenedores, imágenes, volúmenes...

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Introducción%20a%20Docker/2%20Instalación%20de%20Docker%20y%20“hello%20world”/Untitled%206.png)