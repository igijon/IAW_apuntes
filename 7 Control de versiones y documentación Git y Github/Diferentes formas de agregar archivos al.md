#git #github
# Diferentes formas de agregar archivos al escenario

Vamos a trabajar con un nuevo proyecto: `02-bases`

[02-bases.zip](https://drive.google.com/file/d/16ux8u4u2d0azuOqxw7XTcXXByrGlsqnv/view?usp=sharing)

```bash
git init
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled.png)

Imaginemos que desde el último commit se han hecho muchas modificaciones en distintos archivos. Los commits deben estar relacionados con una funcionalidad. Podría dividir commits.

Puedo añadir ficheros de forma individual o añadir ficheros mediante comodines.

```bash
git add *.html
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%201.png)

Puedo hacer el commit:

```bash
git commit -m "archivos html añadidos"
```

Si quiero hacer lo mismo con los js tengo que tener en cuenta la ruta en la que están (dentro de la carpeta js).

```bash
git add js/*.js
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%202.png)

```bash
git commit -m "Archivos JS agregados"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%203.png)

<aside>
💡 Si creo un directorio `new-folder` y el directorio está vacío, con `git status` no lo veremos. Si creo un fichero nuevo dentro, ya sí aparece.

</aside>

```bash
git add css/ #Añade todo lo que hay dentro de la carpeta css
git commit -m "Estilos agregados"
git add . #Añade todo lo demás
git commit -m "Todo lo demás"
```

# VSCode

Vamos a cerrar la carpeta y borrar el `.git` para aprender a trabajar con VSCode.

Abrimos el terminal integrado y hacemos `git init`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%204.png)

Si vamos a la parte de **source control** tenemos:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%205.png)

En la opción `ver como lista` podemos tener la estructura del proyecto e ir añadiendo por partes con staged changes...

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%206.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%207.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%208.png)

<aside>
💡 En VSCode es más rápido pero la consola tiene más control.

</aside>

Si modifico el fichero `index.html` puedo hacer:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Diferentes%20formas%20de%20agregar%20archivos%20al%20escenario/Untitled%209.png)