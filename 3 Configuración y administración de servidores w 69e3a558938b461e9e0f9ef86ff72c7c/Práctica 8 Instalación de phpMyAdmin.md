# Práctica 8: Instalación de phpMyAdmin

@Inma Gijón Cardos 

Aunque muchos usuarios necesitan la funcionalidad de un sistema de gestión de BDD como MySQL, es posible que no se sientan cómodos interactuando con el sistema únicamente desde la consola de MySQL

[phpMyAdmin](https://www.phpmyadmin.net/) se creó con el propósito de que los usuarios puedan interactuar con MySQL a través de una interfaz web. Vamos a ver cómo instalar y proteger phpMyAdmin de modo que podamos utilizarlo de forma segura para gestionar las BDD de un sistema Ubuntu 20.04

Partimos de tener instalado Apache, MySQL y PHP.

# Instalación de phpMyAdmin

```bash
sudo apt update
sudo apt upgrade #Si hay paquetes que instalar
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
```

- `php-mbstring`: módulo para administrar cadenas no-ASCII y convertir cadenas a diferentes codificaciones.
- `php-zip`: esta extensión admite la carga de archivos `.zip` a phpMyAdmin.
- `php-gd`: habilita la obtención de ayuda de [la biblioteca GD Graphics](https://en.wikipedia.org/wiki/GD_Graphics_Library).
- `php-json`: proporciona PHP con compatibilidad para serialización JSON.
- `php-curl`: permite que PHP interactúe con diferentes tipos de servidores utilizando diferentes protocolos.

<aside>
💡 Estas son las opciones que debes elegir cuando  las solicite para configurar correctamente la instalación:

</aside>

<aside>
💡 Para la selección del servidor, elija `apache2` <$>[warning] **Advertencia:** Cuando la línea de comandos aparece, “apache2” está resaltado, pero **no** está seleccionado. Si no pulsa `SPACE` para seleccionar Apache, el instalador *no* moverá los archivos necesarios durante la instalación. Pulse `ESPACIO,` `TAB` y luego `ENTER` para seleccionar Apache. <$>

</aside>

<aside>
💡 Cuando se le pregunte si utiliza `dbconfig-common` para configurar la base de datos, seleccione `Yes`.

</aside>

<aside>
💡 Luego, se le solicitará elegir y confirmar una contraseña para la aplicación de MySQL para phpMyAdmin.

</aside>

Como hemos configurado MySQL habilitando `Validate Password` obtendremos esto:

Para resolver esto, seleccionamos `abortar` para detener el proceso de instalación y hacemos:

```bash
sudo mysql
```

```sql
UNINSTALL COMPONENT "file://component_validate_password";
exit
```

```bash
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
```

 Después, volvemos a habilitarlo:

```bash
sudo mysql
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled.png)

```sql
INSTALL COMPONENT "file://component_validate_password";
exit
```

El proceso de instalación añade el archivo de configuración de phpMyAdmin de Apache al directorio `/etc/apache2/conhable/`, donde se lee de forma automática. Para terminar de configurar Apache y PHP a fin de que funcionen con phpMyAdmin, la única tarea que queda a continuación es habilitar explícitamente la extensión PHP `mbstring`.

```bash
sudo phpenmod mbstring
sudo systemctl restart apache2
```

# Ajuste de la autenticación y privilegios de usuario

Cuando hemos instalado phpMyAdmin, automáticamente se ha creado un usuario de base de datos llamado **phpmyadmin** que realiza ciertos procesos subyacentes para el programa. En vez de registrarse como este usuario con la contraseña administrativa que se estableció durante la instalación, se le recomienda iniciar sesión como **root** user de MySQL o como usuario dedicado a administrar las bases de datos a través de la interfaz de phpMyAdmin.

## Configuración de acceso con contraseña para la cuenta root de MySQL

En los sistemas Ubuntu con MySQL 5.7 (y versiones posteriores), el usuario **root** de MySQL se configura para la autenticación usando el complemento `auth_socket` de manera predeterminada en lugar de una contraseña. En muchos casos, esto proporciona mayor seguridad y utilidad, pero también puede generar complicaciones cuando sea necesario permitir que un programa externo (como phpMyAdmin) acceda al usuario.

Deberemos cambiar el método de autenticación de `auth_socket` a uno que haga uso de una contraseña, para poder acceder a phpMyAdmin como su **root** user de MySQL. Para hacer esto, abra la consola de MySQL desde su terminal:

```bash
sudo mysql
```

```sql
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%201.png)

Efectivamente, el usuario **root** se autentica utilizando el complemento de `auth_socket.` Para configurar la cuenta de **root** de modo que la autenticación se realice con una contraseña, ejecute el siguiente comando `ALTER USER.`Asegúrese de cambiar `password`por una contraseña segura que elija:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%202.png)

```sql
SELECT user,authentication_string,plugin,host FROM mysql.user;
exit
```

Ahora podremos iniciar sesión en la interfaz phpMyAdmin como **root** con la contraseña establecida.

## Configuración del acceso con contraseña para un usuario dedicado de MySQL

Por otra parte, para el flujo de trabajo de algunos proyectos, puede resultar más conveniente la conexión a phpMyAdmin con un usuario dedicado.

```bash
sudo mysql
```

Si tenemos habilitada la autenticación de contraseña para **root** user, como se describe en la sección anterior, deberemos ejecutar el siguiente comando e ingresar su contraseña cuando se le solicite para establecer conexión:

```bash
sudo mysql -u root -p
```

Vamos a crear un usuario nuevo y establecer una contraseña segura:

```bash
CREATE USER 'enrique'@'localhost' IDENTIFIED WITH mysql_native_password BY 'QUser123_';
```

<aside>
💡 Podríamos utilizar `caching_sha2_password`, pero con versiones de PHP anteriores a la 7.4 da algunos problemas, por tanto lo haremos con `mysql_native_password`

</aside>

Le damos privilegios

```bash
GRANT ALL PRIVILEGES ON *.* TO 'enrique'@'localhost' WITH GRANT OPTION;
```

Ahora podremos acceder a la interfaz web visitando:

`https://dominio_o_ip_publica/phpmyadmin`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%203.png)

Iniciamos sesión como root con el nombre de usuario y contraseña que configuramos:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%204.png)

## Protección de la instancia de phpMyAdmin

Debemos tomar medidas adicionales para evitar el acceso no autorizado. Una opción para hacer esto es disponer una puerta de enlace delante de toda la aplicación utilizando las funciones de autenticación y autorización de `.htaccess` integradas de Apache.

Para hacerlo, primero debemos habilitar el uso de anulaciones del archivo `.htaccess` editando su archivo de configuración de Apache.

Utilice su editor de texto preferido para editar el archivo `phpmyadmin.conf` que se encuentra ahora en el directorio de configuración de Apache. En este caso, utilizaremos `nano`:

```bash
sudo nano /etc/apache2/conf-available/phpmyadmin.conf
```

Agregamos una directiva `AllowOverride All` dentro de la sección `<Directory /usr/share/phpmyadmin>`

del archivo de configuración:

```bash
sudo systemctl restart apache2
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%205.png)

Ahora que hemos habilitado el uso de `.htaccess` para nuestra aplicación, debemos crear uno para implementar seguridad.

Para hacerlo de forma correcta, el archivo debe crearse dentro del directorio de la aplicación. Podemos crear el archivo necesario y abrirlo en su editor de texto con privilegios root escribiendo lo siguiente:

```bash
sudo nano /usr/share/phpmyadmin/.htaccess
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%206.png)

Cada una de estas líneas, indica:

- `AuthType Basic`: en esta línea se especifica el tipo de autenticación que implementará. Con este tipo se implementará la autenticación de contraseña utilizando un archivo de contraseña.
- `AuthName:` establece el mensaje para el cuadro de diálogo de autenticación. Debe procurar que esto sea genérico para que los usuarios no autorizados no obtengan información sobre lo que se protege.
- `AuthUserFile`: establece la ubicación del archivo de contraseña que se utilizará para la autenticación. Esto debe quedar fuera de los directorios que se presentan. Crearemos este archivo pronto.
- `Require valid-user`: especifica que solo los usuarios autenticados deberán tener acceso al recurso. Esto es lo que realmente impide el ingreso de los usuarios no autorizados.

Cuando termine, guarde y cierre el archivo.

La ubicación que seleccionó para su archivo de contraseña fue `/etc/phpmyadmin/.htpasswd`. Ahora puede crear este archivo y pasarle un usuario inicial con la utilidad `htpasswd`:

```bash
sudo htpasswd -c /etc/phpmyadmin/.htpasswd username
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%207.png)

Ahora, al acceder al subdirectorio phpMyAdmin, se le solicitarán el nombre de cuenta y la contraseña adicionales que acaba de configurar.

`http://dominio_o_ip/phpmyadmin`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%208%20Instalación%20de%20phpMyAdmin/Untitled%208.png)