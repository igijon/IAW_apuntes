# Servidor web Apache
#apache


@Inma Gijón Cardos 

---

Un servidor web es un programa que se ejecuta de forma continua en un ordenador (también se utiliza el término para referirse al ordenador que lo ejecuta), se mantiene a la espera de peticiones por parte de un cliente (un navegador de Internet) y contesta a estas peticiones de forma adecuada, sirviendo una página web que será mostrada en el navegador o mostrando el mensaje correspondiente si se detectó algún error.

Uno de los servidores web más populares del mercado y el más utilizado actualmente es Apache, de código abierto y gratuito, disponible para Windows y GNU/Linux, entre otros.

En cuanto a su arquitectura podemos destacar lo siguiente:

- Estructurado en módulos
- Cada módulo contiene un conjunto de funciones relativas a un aspecto concreto del servidor
- El archivo binario **httpd** contiene un conjunto de módulos que han sido compilados
- La funcionalidad de estos módulos puede ser activada o desactivada al arrancar el servidor

- Los módulos de apache se pueden clasificar en tres categorías:
    - Módulos base: funciones básicas
    - Módulos multiproceso: encargados de la unión de los puertos de la máquina, aceptando peticiones y atendiéndolas.
    - Módulos adicionales: se encargan de añadir funcionalidad al servidor.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/2%20World%20Wide%20Web/Servidor%20web%20Apache/Untitled.png)

El servidor Apache se desarrolla dentro del proyecto HTTP Server (httpd) de la Apache Software Foundation. La licencia de software, bajo la cual el software de la fundación Apache es distribuido, es una parte distintiva de la historia de Apache HTTP Server y de la comunidad de código abierto. La **Licencia Apache** permite la distribución de derivados de código abierto y cerrado a partir de su código fuente original.

<aside>
💡 [https://httpd.apache.org/](https://httpd.apache.org/)

</aside>