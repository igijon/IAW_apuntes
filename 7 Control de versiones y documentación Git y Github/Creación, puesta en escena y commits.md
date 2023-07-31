#git #github
# Creación, puesta en escena y commits

Nos creamos un archivo `[readme.md](http://readme.md)` en markdown (especialmente utilizado en **Github).**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled.png)

```bash
git add . #Añadimos al stage
git reset README.md #Si quiero sacarlo del stage
git add .
git commit -m "Readme agregado"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%201.png)

Si modifico el fichero:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%202.png)

```bash
git commit -am "Readme actualizado"
git log
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%203.png)

El hash del commit es único. El **HEAD** apunta a la última versión del repositorio. En este caso apunta a `main`. Después, podemos ver el autor que es importante para saber quién hizo el commit y la fecha. 

<aside>
💡 El texto del commit debe ser muy descriptivo.

</aside>

Los commit están ordenados de el más reciente al más antiguo.

<aside>
💡 En VSCode, si tenéis instalada la **activitus bar**, veremos que tenemos la parte de git abajo.

</aside>

<aside>
💡 Instalar también la extensión **git graph**

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%204.png)

Si modifico de nuevo [`readme.md`](http://readme.md) e `index.html`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%205.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%206.png)

Desde el **source control** tengo:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%207.png)

Podríamos descartar cambios, hacer el add del stage... es decir no añadirlo o sí... (esto sería almacenar cambios provisionalmente pero aún no se ha hecho commit).

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Creación,%20puesta%20en%20escena%20y%20commits/Untitled%208.png)