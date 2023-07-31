#git #github 

# Fundamentos de Git

# Control de versiones

Control de versiones, es la práctica de rastrear y gestionar los cambios en el código de software. Los sistemas de control de versiones, son herramientas software que ayudan a los equipos de desarrollo a gestionar los cambios en el código fuente a lo largo del tiempo. A medida que los entornos de desarrollo se aceleran los sistemas de control de versiones ayudan a los equipos de desarrollo a trabajar de forma más rápida e inteligente.

El software de control de versiones realiza un seguimiento de todas las modificaciones en el código en un tipo especial de base de datos. Si se comete un error, los desarrolladores pueden ir hacia atrás en el tiempo.

Las principales ventajas de un sistema de control de versiones:

- Proporciona un completo **historial de cambios** a largo plazo de todos los archivos.
- Permite crear **ramas y fusiones**.
- **Trazabilidad.**

# Qué es Git

Con diferencia, actualmente, Git es el sistema de control de versiones más utilizado del mundo. 

Es un proyecto de código abierto maduro y con mantenimiento activo que desarrolló originalmente Linus Tovalds, el famoso creador del kernel del sistema operativo Linux (2005).

[Qué es el control de versiones | Atlassian Git Tutorial](https://www.atlassian.com/es/git/tutorials/what-is-version-control)

[Qué es Git: conviértete en todo un experto en Git con esta guía](https://www.atlassian.com/es/git/tutorials/what-is-git)

# Fundamentos de Git

Si no tenemos **git** instalado, lo instalaremos dependiendo de nuestra plataforma.

[Git](https://git-scm.com/)

## Primeros comandos

```bash
git --version
git help [comando]
git config --global user.name “Inma Gijón”
git config —-global user.email “igijoninf@gmail.com”
# A nivel de repositorio igual pero sin --global
git config —-global -e
#(Para insertar, pulsar a, modificar lo que queramos, después esc+:wq!)
```

## Primer repositorio

Un proyecto equivale a un repositorio en Git.

Vamos a partir de este proyecto:

[01-bases.zip](https://drive.google.com/file/d/1l6askpE8J1DtesTESl9w-PBZyC4hJexs/view?usp=sharing)

`01-bases` va a ser mi primer repositorio. En el terminal entramos en el path:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled.png)

Si aparece este warning, es porque Git desde hace tiempo quiere cambiar el nombre de **master** por **main** porque master parece ofensivo en estos tiempos por el concepto de **master-esclavo** y lo políticamente incorrecto... Antes la rama principal se llamaba master.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%201.png)

Se puede hacer la configuración global para que la rama por defecto sea la que se establece (lo indica en el warning).

Una vez inicializado el repositorio, si mostramos los archivos ocultos:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%202.png)

Veremos un directorio oculto `.git` que no debemos tocar. Si lo borramos, borramos el repositorio. Todo lo que haremos relacionado con el control de versiones, estará almacenado en .git.

```bash
git status #Indica la rama en la que estamos, los archivos a los que no les damos seguimiento...
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%203.png)

Si hago:

```bash
git add index.html
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%204.png)

Me indica que el fichero añadido está listo para hacer `commit`, es decir, para tomarle la foto de su estado.

```bash
git add .
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%205.png)

Si quiero borrar por ejemplo `.DS_Store`

```bash
git reset .DS_Store
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%206.png)

Lo añado de nuevo y hago la foto:

```bash
git add .
git commit -m "Primer commit"
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%207.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%208.png)

Desde el último commit no ha habido cambios.

<aside>
💡 Normalmente hacemos commit cuando terminamos una funcionalidad relevante.

</aside>

```bash
git log
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%209.png)

A veces hay problemas con la interpretación del CRLF, básicamente es la interpretación de un carácter, lo podemos solucionar mediante:

```bash
git config code.autocrlf true
```

Si abrimos nuestro proyecto e VSCode y modificamos el `index.html`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%2010.png)

```bash
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%2011.png)

Si queremos reconstruir el proyecto a cómo estaba en el último commit haremos:

```bash
git checkout -- .
```

Esto afecta a todos los ficheros a los que se les da seguimiento, si alguno es `untracked` (está en .gitignore... por ejemplo), esto no afecta.

# Cambiar nombre de la rama master a main

Una rama es un lugar en el que nos encontramos trabajando. Hacen la analogía de un árbol (podemos imaginar que nosotros somos hormigas y estamos en una u otra rama).

No es nada recomendable trabajar en Master... se debe tener ahí sólo una versión definitiva, por ejemplo lo que iría a **producción.**

```bash
git branch
git branch -m master main
git branch
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%2012.png)

Si quiero establecerla como rama principal siempre:

```bash
git config --global init.defaultBranch main
```

Para estar seguros de que esta configuración es correcta, puedo borrar el directorio `.git`que hay dentro del proyecto.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%2013.png)

```bash
git init
git status
git branch
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%2014.png)

```bash
git config --global -e
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Fundamentos%20de%20Git/Untitled%2015.png)

Para salir `:q!`. Si queremos escribir `:wq!`