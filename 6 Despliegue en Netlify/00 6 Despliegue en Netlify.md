#netlify

# 6. Despliegue en Netlify

@Inma Gijón Cardos 

Abrimos en **VSCode** el proyecto **vue_pokemon_game** clonado según indicamos aquí:

[Inicios en Github](https://www.notion.so/Inicios-en-Github-1413b39a744f4d33afd76e17d36bcf18#fd49653b78e647abbb0b1adf96401fbe)

Es un proyecto del lado de cliente desarrollado utilizando **[Vue](https://vuejs.org/)**

[Vue.js - The Progressive JavaScript Framework | Vue.js](https://vuejs.org/)

Lo primero que necesito es abrir el terminal para preparar lo que necesitamos para ejecutar este proyecto:

Instalaremos **Node.js** porque lo necesitamos como entorno de ejecución de JavaScript y gestor de paquetes:

[Node.js](https://nodejs.org/es/)

Posteriormente, este proyecto se ha creado con `yarn` por lo tanto tenemos que instalarlo también. Yarn es un gestor de dependencias JavaScript creado por Facebook en colaboración con Google.

[Yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)

```bash
npm install --global yarn
```

Una vez instalado, instalamos `vue`. Para ello:

[Installation | Vue CLI](https://cli.vuejs.org/guide/installation.html)

```bash
yarn global add @vue/cli
#Para Windows
#npm install --global vue-cli
```

Comprobamos la instalación con:

```bash
vue --version
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled.png)

Para construir el proyecto, podemos abrirlo en VSCode (o hacerlo en el terminal):

```bash
yarn install
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%201.png)

Para ejecutarlo en local:

```bash
yarn serve
```

Todos estos comandos están configurados en el fichero package.json.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%202.png)

Esto levanta nuestra aplicación en el puerto 8080:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%203.png)

Este proyecto consume un API REST gratuita:

[PokéAPI](https://pokeapi.co/)

Lo que haremos ahora será desplegar en **Netlify**, para ello, en primer lugar debemos tener una cuenta, podemos hacer login con nuestra cuenta de **Github.**

[Netlify: Develop & deploy the best web experiences in record time](https://www.netlify.com/)

Tenemos varias opciones para desplegar: manual o configurando un despliegue automático a partir de un repositorio.

# Despliegue manual Netlify

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%204.png)

Nos aparecerá algo como esto:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%205.png)

Para generar la carpeta del proyecto a desplegar, nos vamos a VSCode:

```bash
yarn build
```

Esto genera una carpeta `dist`en el directorio del proyecto. Será esta carpeta la que arrastremos:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%206.png)

Esperaremos hasta que esté desplegado:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%207.png)

En `Site settings` podemos cambiar el nombre:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%208.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%209.png)

Ya tenemos nuestro sitio desplegado:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2010.png)

<aside>
💡 En `Site settings` también podemos eliminar el sitio web.

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2011.png)

# Despliegue a partir de un repositorio remoto

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2012.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2013.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2014.png)

Seleccionamos el repositorio y la rama a desplegar.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2015.png)

**Iniciamos el despliegue.**

También podemos cambiarle el nombre:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2016.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2017.png)

# Comprobación push - despliegue

Abrimos nuestro proyecto en VSCode.

Vamos a editar el fichero `src/pages/PokemonPage.vue` añadiendo un título más:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2018.png)

Haremos el `commit` y `push` correspondiente:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2019.png)

Si refrescamos la página de Netlify, veremos que comienza un nuevo despliegue, que sólo se llevará a cabo si se realiza correctamente:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2020.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/6%20Despliegue%20en%20Netlify/Untitled%2021.png)