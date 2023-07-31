
#despliegue #php #laravel #mysql

# 5. Despliegue de un proyecto PHP Laravel, MySQL

@Inma Gijón Cardos 

- Carpeta en /var/www/html
- Propietario inmagijon:inmagijon (usuario_linux:grupo_linux)

```bash
sudo chown -R inmagijon:inmagijon path
```

- Transferir ficheros y .sql por ftp

Para crear una BDD nueva ejecutamos:

```sql
mysql -u root -p
mysql> CREATE DATABASE example_laravel;
```

Ahora vamos a crear un usuario y concederle privilegios completos sobre la BDD personalizada que acabamos de crear. Elige una contraseña segura.

```sql
CREATE USER 'laravel_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Luser123_';
```

Ahora, le daremos permiso a este usuario sobre la BDD:

```sql
GRANT ALL PRIVILEGES ON example_laravel.* TO 'laravel_user'@'localhost';
FLUSH PRIVILEGES;
```

Con esto, el usuario tendrá privilegios completos sobre la BDD y evitará que el usuario cree o modifique otras BDD de su servidor.

Cerramos el shell de MySQL:

```sql
exit
```

Restauramos la BDD a partir del fichero `.sql`

```bash
cd /var/www/html/ejemploLaravelMySQL
mysql -u laravel_user -p example_laravel < ejemploQB.sql
mysql -u laravel_user -p
```

```bash
USE example_laravel;
SHOW TABLES;
```

Falta editar el fichero `.env` del proyecto Laravel para indicar los datos de la BDD. Es un fichero oculto.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/5%20Despliegue%20de%20un%20proyecto%20PHP%20Laravel,%20MySQL/Untitled.png)

Nos queda modificar el fichero `.conf` de apache indicando lo siguiente (podemos crear un fichero laravel.conf, por ejemplo):

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/5%20Despliegue%20de%20un%20proyecto%20PHP%20Laravel,%20MySQL/Untitled%201.png)

Con los certificados correctos, para configurar https en su momento tendríamos que añadir la parte correspondiente tal y como hemos visto en ejemplos anteriores.

Habilitamos únicamente ese sitio.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/5%20Despliegue%20de%20un%20proyecto%20PHP%20Laravel,%20MySQL/Untitled%202.png)

Para la generación de las vistas de Laravel en el proyecto tenemos que dar permisos a esa carpeta:

```bash
cd /var/www/html
sudo chmod 777 -R ejemploLaravelMySQL
```

```bash
sudo a2dissite 000-default.conf #deshabilita el conf de un sitio... haremos esto con todos
sudo a2ensite laravel.conf #habilita el sitio que estamos desplegando
sudo a2enmod rewrite
sudo systemctl restart apache2
```

Desde el anfitrión podemos ver que podemos acceder y está todo montado:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/5%20Despliegue%20de%20un%20proyecto%20PHP%20Laravel,%20MySQL/Untitled%203.png)