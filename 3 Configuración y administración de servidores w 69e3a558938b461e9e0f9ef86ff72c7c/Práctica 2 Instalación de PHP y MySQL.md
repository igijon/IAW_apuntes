# Práctica 2: Instalación de PHP y MySQL

# INSTALACIÓN DE MYSQL

Ahora que disponemos de un servidor web funcional, vamos a ver cómo instalar un sistema de BDD para poder almacenar y gestionar datos de nuestro sitio. MySQL es un sistema de administración de BDD popular que se utiliza con PHP.

```bash
sudo apt install mysql-server
```

Cuando la instalación se complete, se recomienda ejecutar una secuencia de comandos de seguridad que viene preinstalada en MySQL. Con esta secuencia de comandos se eliminarán algunos ajustes predeterminados poco seguros y se bloqueará el acceso a su sistema de BDD. 

```bash
sudo mysql_secure_installation
```

Nos preguntará si deseamos configurar el `VALIDATE PASSWORD PLUGIN`

<aside>
💡 La habilitación de esta característica queda a discreción del usuario. Si se habiilta, MySQL rechazará con un mensaje de error las contraseñas que no coincidan con los criterios especificados. Dejar la validación desactivada será una opción segura, pero siempre deberá utilizar contraseñas seguras y únicas para credenciales de BDD.y

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%202%20Instalación%20de%20PHP%20y%20MySQL/Untitled.png)

Si responde `y` se le solicitará un nivel de validación de contraseña. Si ingresa 2 indicará que es el nivel más seguro y recibirá mensajes de error al intentar establecer cualquier contraseña que no contenga números, letras en mayúscula y minúscula y caracteres especiales, o que se base en palabras comunes de diccionario.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%202%20Instalación%20de%20PHP%20y%20MySQL/Untitled%201.png)

Después nos pide una contraseña para el `root user` de MySQL. 

<aside>
💡 No confundir con el **root del sistema**. El **root user de BDD** es un usuario administrativo con privilegios completos sobre el sistema de base de datos. Si bien el método de autenticación predeterminado del root user de MySQL no requiere el uso de una contraseña, **incluso si hay una establecida**, deberá definir una contraseña segura en este punto como una medida de seguridad adicional.

</aside>

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%202%20Instalación%20de%20PHP%20y%20MySQL/Untitled%202.png)

Para el resto de preguntas, presione `y` y `enter`. Con esto, se eliminarán algunos usuarios anónimos y la base de datos de prueba, se deshabilitarán las credenciales de inicio de sesión remoto de root y se cargarán estas nuevas reglas para que MySQL aplique de inmediato los cambios que realizó.

Cuando terminemos comprobamos si podemos iniciar sesión en la consola de MySQL

```bash
sudo mysql
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%202%20Instalación%20de%20PHP%20y%20MySQL/Untitled%203.png)

Para salir de la consola

```bash
mysql> exit
```

Observa que no necesitaste proporcionar una contraseña para conectarte como **root user**, a pesar de que se definió una al ejecutar la secuencia de comandos **mysql_secure_installation**. Esto se debe a que el método de autenticación predeterminado para el usuario administrativo es **unix_socket** en ver de **password.** Si bien esto puede parecer un problema de seguridad inicialmente, hace que el servidor de la BDD sea más seguro porque los únicos usuarios que pueden iniciar sesión como **root user** de MySQL son los usuarios del sistema con privilegios sudo que establecen conexión desde la consola o mediante una aplicación que se ejecute con los mismo privilegios.

Esto significa que no podrá usar el usuario **root** de la BDD administrativa para establecer conexión desde su aplicación PHP.

Establecer una contraseña para la cuenta **root** de MySQL es una medida de protección, en caso de que el método de autenticación predeterminado se cambie de **unix_socket** a **password.**

<aside>
💡 Para mayor seguridad, es mejor disponer de cuentas de usuario dedicadas con privilegios de menor alcance configurados para cada BDD, en especial si planea disponer de varias BBDD alojadas en el servidor.

</aside>

# INSTALACIÓN DE PHP

Tenemos instalado **Apache** para presentar el contenido, **MySQL** para almacenar y gestionar los datos. **PHP** es el componente de nuestra configuración que procesará el código para mostrar contenido dinámico al usuario final.

```bash
sudo apt install php libapache2-mod-php php-mysql
```

**libapache2-mod-php** habilita Apache para gestionar archivos PHP.

**php-mysql** permite que PHP se comunique con BDD basadas en MySQL.

Confirmamos la versión de php:

```bash
php -v
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%202%20Instalación%20de%20PHP%20y%20MySQL/Untitled%204.png)

[Cómo instalar la pila Linux, Apache, MySQL y PHP (LAMP) en Ubuntu 20.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04-es)