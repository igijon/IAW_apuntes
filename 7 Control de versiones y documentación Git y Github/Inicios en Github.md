#git #github 

# Inicios en Github

Plataforma controlada por **Microsoft.**

Se pueden manejar repositorios, proyectos, equipos, organizaciones...

# Repositorio remoto, push y pull

Respaldo remoto de nuestro repositorio.

Para que nuestros cambios se suban al servidor se realiza una operación `push`.

Para obtener los cambios de nuestro repositorio remoto al repositorio local deberemos hacer `pull`.

Git no maneja el acceso al repositorio, los servicios que permiten controlar eso son por ejemplo:

- Github
- Bitbucket...

**Github es tan usado por la potencia gratuita que nos ofrece.**

<aside>
💡 Un repositorio público permite ser clonado a otras personas aunque no colaborar.

</aside>

<aside>
💡 Un repositorio privado no podrá ser visto ni clonado.

</aside>

# Creación de cuenta en Github

[GitHub: Where the world builds software](https://github.com/)

- Establecemos un correo válido
- Establecemos un **username** (no se puede cambiar, es mejor asegurarse de elegir algo que os guste).
- Os pedirá resolver un acertijo para asegurarse de que no somos un bot.
- Os mandarán un código de 6 letras al mail.
- Se creará la cuenta!!!

<aside>
💡 Se puede cambiar la apariencia. Modo oscuro, etc.

</aside>

# Información detallada en el perfil

- Crear un repositorio en Github con el nombre del usuario.
- En el repositorio, crear un fichero `[README.md](http://README.md)` con el contenido a visualizar.
- Os dejo abajo un link para familiarizarnos con la sintaxis de **markdown.**

[Sintaxis Markdown al completo - Cheatsheet en español](https://markdown.es/sintaxis-markdown/)

# Push

Descargamos el **ejemplo** y lo abrimos en VSCode.

[https://drive.google.com/file/d/1JNkUYRZQf110fF9VlC3WyD_h0qrAA6eT/view?usp=sharing](https://drive.google.com/file/d/1JNkUYRZQf110fF9VlC3WyD_h0qrAA6eT/view?usp=sharing)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled.png)

Para tener nuestro repositorio a salvo, necesitamos un repositorio remoto: **Github, Bitbucket...** 

Abrimos **Github y vamos a crear un nuevo repositorio:**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%201.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%202.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%203.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%204.png)

En nuestro caso queremos la segunda opción, es decir, hacer **push** de un repositorio existente. Copiamos el código:

```bash
git remote add origin https://github.com/igijon/liga-justicia.git
git branch -M main
git push -u origin main
```

<aside>
💡 Debéis seleccionar vuestro repo no el mío!!!

</aside>

Si es la primera vez que hacemos algo así, nos pedirá que nos identifiquemos. Esto es igual en todos, abrirá el sitio web para autorizar el acceso y diremos que sí. **`Authorize Github.` Seguimos los pasos.** 

Una vez que hemos terminado se hará el **push al repositorio remoto.**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%205.png)

```bash
git push
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%206.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%207.png)

# Pull de los últimos cambios en el repositorio de Github

<aside>
💡 No es común editar desde Github, pero haremos el ejemplo para ver que hay cosas en el repo que no tengo en local.

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%208.png)

<aside>
💡 No haremos commits directamente en main!!!! Pero esto es sólo un ejemplo...

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%209.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2010.png)

Podemos pensar que cualquier desarrollador del equiipo ha podido hacer **push** y subido cambios al repo, pero yo  no los tengo en local. Para traerlos:

```bash
git pull
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2011.png)

```bash
git remote -v #Obtengo el path de nuestro repositorio
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2012.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2013.png)

<aside>
💡 En algunas ocasiones, se produce un `warning` al hacer pull porque nos pide configurar de qué modo integra los contenidos del repositorio local y el remoto. Vamos a ver cómo configurar esto.

</aside>

<aside>
💡 Por seguridad, sólo nos interesa que git traiga los cambios de remoto si se puede realizar un **fast-forward** y si no, entre en modo conflicto y nos pregunte.

</aside>

```bash
git config --global pull.ff only #quiero que cuando se haga el pull, use fast forward únicamente 
```

# Subir cambios locales al repositorio remoto

Vamos a modificar el fichero **README.md.**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2014.png)

Hago el commit:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2015.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2016.png)

Me está indicando que la información difiere del repositorio remoto, que sólo la rama main en local está en el último commit pero el remoto (**origin/main)** se encuentra un commit anterior.

```bash
git push #para subir los cambios.
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2017.png)

Vamos a editar el [README.md](http://README.md) desde Github.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2018.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2019.png)

También voy a modificar el mismo fichero desde local:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2020.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2021.png)

```bash
git pull
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2022.png)

Hay un problema porque no puede hacer **fast-forward** directamente.

La estrategia recomendada en este caso sería:

```bash
git config pull.rebase true #Esto hace una configuración por defecto para el repositorio local
# git config --global pull.rebase true para # Para que la configuración sea global
# git pull --rebase en Windows
git pull
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2023.png)

<aside>
💡 Estamos en medio de un rebase, no estoy en una rama, estoy en un rebase del main.

</aside>

<aside>
💡 A veces, necesitamos corregir mensajes en commits, organizar commits, unir commits, reorganizar ramas... para ello se utiliza un **`rebase`**

</aside>

Acepto ambos cambios y hacemos un commit:

```bash
git status
git commit -am "Readme unificado con origin main"
git status
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2024.png)

Tengo que continuar el **rebase.**

```bash
git rebase --continue #Si estamos satisfechos con los cambios
git push
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2025.png)

# Clonar un repositorio

Vamos a aprender a clonar un repositorio diferente (para una práctica posterior en el punto siguiente):

[GitHub - igijon/vue_pokemon_game: Juego de Pokemon con Vue](https://github.com/igijon/vue_pokemon_game)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2026.png)

Copiamos el link de nuestro repositorio a clonar.

Abro el terminal y me **sitúo en la carpeta en la que quiero clonar el repositorio:**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Inicios%20en%20Github/Untitled%2027.png)

Si os situais en el directorio, veréis que se ha descargado y descomprimido el repositorio para ser utilizado y contiene al hacer `git log` todos los commits correspondientes.

# Enlaces interesantes

[Almacenar tus credenciales de GitHub en el caché dentro de Git - GitHub Docs](https://docs.github.com/es/get-started/getting-started-with-git/caching-your-github-credentials-in-git#platform-linux)

[Almacenar tus credenciales de GitHub en el caché dentro de Git - GitHub Docs](https://docs.github.com/es/get-started/getting-started-with-git/caching-your-github-credentials-in-git#platform-windows)

[igijon - Overview](http://github.com/igijon)

[Build your own octocat](https://myoctocat.com/)