#git #github 

# Viajes en el tiempo

# Preparando el proyecto

[03-material-heroes.zip](https://drive.google.com/file/d/1cnA3rIjzzEkT7EP5oHAFbT8-vIcgQUpE/view?usp=sharing)

Vamos a descomprimir este proyecto, inicializar el repositorio e ir añadiendo por orden los siguientes ficheros.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled.png)

<aside>
💡 Es importante que se agreguen los ficheros por orden por lo que haremos después

</aside>

Nos damos cuenta que en historia tenemos batman y superman, podemos cambiar el commit indicando:

```bash
git commit --amend
```

Entra en modo edición y para añadir o borrar pulsamos `a`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%201.png)

Para salir, `ESC` + `:wq!`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%202.png)

Vamos a añadir un nuevo héroe:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%203.png)

```bash
git commit -am "Agregamos a Linterna Verde"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%204.png)

# Viajes, reset y reflog

Imaginemos que nos damos cuenta de que no sólo queríamos añadir a Linterna verde, sino que también queremos añadir a Robin en ese commit. Podemos hacer:

```bash
git reset --soft 4437ab3bf06d5b6aba8315e1066541b5e3961e92 #Los hash son únicos, en este caso son los de mi ejemplo, no hay dos iguales
```

Nos situamos en el commit anterior al que habíamos hecho con la modificación de Linterna Verde. Si nos fijamos, en VSCode, aparecerá **[heroes.md](http://heroes.md)** como M.

Modificamos **heroes.md**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%205.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%206.png)

Imaginemos ahora que me doy cuenta de que el proyecto no va bien y que quiero volver al punto en el que agregamos las ciudades porque en ese punto he detectado que todo está estable. Para hacer eso cojo el hash del commit donde agregué las ciudades, voy a modificar `—soft` (mantiene todos los cambios) por `—mixed` (no elimina los cambios pero saca todo del stage)

```bash
git reset --mixed 33271b7597b409857bf7cfc490373259d95b586f
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%207.png)

Después de hacer esto nos damos cuenta de que toda la carpeta historia aparece como untracked (U)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%208.png)

Podría descartar todos esos cambios haciendo

```bash
git reset --hard 33271b7597b409857bf7cfc490373259d95b586f
```

Este en principio es “destructivo”. Si refresco, eh **[heroes.md](http://heroes.md)** ya no tengo los cambios.

Si me muevo al punto en el que agregamos las misiones puedo hacer:

```bash
git reset --hard 45b81442745dbeb1010f9d474d0df8c421ad972e
```

Imaginemos que viene nuestro responsable y nos dice que todo estaba bien... ¿qué hacemos?

<aside>
💡 Git no pierde nada!

</aside>

```bash
git reflog #Referencias de todo lo que ha sucedido en orden cronológico
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%209.png)

Yo puedo regresar por ejemplo al punto donde añadimos a Robin y Linterna Verde.

```bash
git reset --hard 473db20
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Viajes%20en%20el%20tiempo/Untitled%2010.png)

<aside>
💡 Para evitar este tipo de cosas... debemos trabajar en ramas distintas y cuando nos aseguremos de que todo es correcto se fusionarán como veremos después

</aside>