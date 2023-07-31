#git #github 

# Ramas, uniones, conflictos

# Merge: Fast forward

Git detecta que no hay cambios en la rama principal y los cambios de la rama se pueden integrar como si no hubiésemos ramificado.

[demo-06.zip](https://drive.google.com/file/d/19IhZjbqs3ub_ozGLKEzhC1_CLcEhbq7q/view?usp=sharing)

```bash
git log
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled.png)

Si alguien me pide una funcionalidad nueva, relacionada con **villanos.**

Me creo un fichero **villanos.md**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%201.png)

Para no influir en **main** vamos a crear una rama... este fichero aún es **untracked.**

```bash
git branch rama-villanos
git branch
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%202.png)

```bash
git checkout rama-villanos
git log #Nos indica que HEAD es rama-villanos y apunta al mismo sitio que master
git add .
git commit -am "Villanos agregados"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%203.png)

Modifico **villanos.md**

```markdown
1. Lex Luthor
2. Joker
3. Flash Reverso
```

```bash
git commit -am "Flash Reverso añadido"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%204.png)

Una vez que decido que está todo bien, quiero mezclar con master... es decir fusionar el contenido de la rama-villanos con master.

Por comandos:

```bash
git checkout master #Me muevo a master, ahí no tengo villanos.md
#Tengo que posicionarme en la rama que va a esperar los cambios, es decir, en master (main)
git merge rama-villanos #Se trae los contenidos de rama-villanos a master. Git logra identificar todos los cambios sin conflictos
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%205.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%206.png)

# Merge: Uniones automáticas

Si los cambios de unas y otras no coinciden pues Git puede hacer el merge sin problema.

Voy a modificar el fichero **[villanos.md](http://villanos.md)** creando otra rama... lo hago de forma visual y en un paso (creación y moverme).

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%207.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%208.png)

```markdown
1. Lex Luthor
2. Joker
3. Flash Reverso
4. Doomsday
```

```markdown
git commit -am "Agregamos a Doomsday"
```

```markdown
1. Lex Luthor
2. Joker
3. Flash Reverso
4. Doomsday

## Notas
```

```markdown
git commit -am "Notas en villanos"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%209.png)

Imaginad que me dicen en mi trabajo que la aplicación estable (la que está en **master),** necesita borrar a **Daredevil** porque no era de DC del fichero **heroes.md**...

Voy a máster y modifico el fichero **heroes.md**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2010.png)

```markdown
# Heroes

* Superman
* Batman
* Aquaman
* Mujer Maravilla
* Linterna Verde
* Robin
```

```markdown
git commit -am "Borramos a Daredevil"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2011.png)

Las dos ramas han avanzado en su línea del tiempo.

Imaginemos que es el momento de unir los cambios de **nuevos-villanos** con la rama master. 

<aside>
💡 Tengo que estar posicionado en la rama que quiero que reciba los cambios, en este caso **master.**

</aside>

```bash
git merge nuevos-villanos #Git me pide indicar el mensaje para un commit indicando el merge
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2012.png)

<aside>
💡 Para salir `ESC+:wq!`

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2013.png)

# Merge: Manual

Si las dos ramas han ido evolucionando por su lado y hay conflictos, Git nos pedirá resolverlos de forma manual y Git crea un commit nuevo **merge commit.**

Vamos a causar un conflicto como ejemplo.

<aside>
💡 Un conflicto es un código que Git no es capaz de resolver de forma automática y pide la resolución de forma manual al usuario.

</aside>

Creo una nueva rama: **`rama-conflicto`**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2014.png)

Voy a modificar el fichero **misiones.md:**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2015.png)

```bash
git commit -am "Misiones actualizadas"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2016.png)

Voy a regresar a **`master`**

<aside>
💡 NO DEBEMOS TRABAJAR EN MASTER, ESTO ES SÓLO UN EJEMPLO.

</aside>

Realizo las siguientes modificaciones en **misiones.md:**

```markdown
	# Misiones

1. Acabar con el plan de Lex Luthor.
2. Crear la liga de la justicia.
3. Buscar nuevos miembros que luchen por la justicia.
4. Buscar comida para ellos.
```

<aside>
💡 Funciona super bien con GIT pero con imágenes por ejemplo, compara en binario.

</aside>

```markdown
git commit -am "Misiones actualizadas master"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2017.png)

Si intento hacer el **merge:**

```bash
git merge rama-conflicto
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2018.png)

<aside>
💡 Los ficheros que no den conflicto van a pasar sin problema.

</aside>

Tenemos que resolver los conflictos y después indicar en el commit qué ha pasado.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2019.png)

Nos indica qué cambio queremos quedarnos.

En VSCode tenemos opciones para seleccionar lo que quiero hacer...

De forma manual se resolvería seleccionando qué es lo que dejo y tocar el md, dejándolo así. Finalmente guardo.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2020.png)

Si miro `git status:`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2021.png)

Para resolver el conflicto, tenemos que hacer el commit:

```bash
git commit -am "Unión con rama conflicto"
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Ramas,%20uniones,%20conflictos/Untitled%2022.png)