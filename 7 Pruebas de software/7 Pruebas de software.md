#testing


# 7. Pruebas de software

@Inma Gijón Cardos 

[Pruebas de software - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/Pruebas_de_software)

[¿Qué tipos de pruebas de software son habituales para un desarrollador? - campusMVP.es](https://www.campusmvp.es/recursos/post/que-tipos-de-pruebas-de-software-son-habituales-para-un-desarrollador.aspx)

# Ejemplo de pruebas unitarias en el proyecto de Vue-Pokemon

Como ejemplo de **test unitarios** podemos ver en el proyecto que existe una carpeta: **tests/unit**

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Pruebas%20de%20software/Untitled.png)

En esta carpeta se reproduce la estructura del proyecto que afecta a los archivos que se van a testear.

En este proyecto para pruebas, se ha utilizado el framework de pruebas **Jest**

[Jest · 🃏 Delightful JavaScript Testing](https://jestjs.io/es-ES/)

Los ficheros de pruebas tienen la nomenclatura `*.spec.js`

Por ejemplo, el fichero de pruebas sobre ***PokemonPage.vue*** se llama ***PokemonPage.spec.js***

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Pruebas%20de%20software/Untitled%201.png)

Para ejecutar los test:

```bash
yarn test:unit
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Pruebas%20de%20software/Untitled%202.png)