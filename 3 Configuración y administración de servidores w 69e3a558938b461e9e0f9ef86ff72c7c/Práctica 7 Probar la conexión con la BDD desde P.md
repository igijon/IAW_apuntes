# Práctica 7: Probar la conexión con la BDD desde PHP

@Inma Gijón Cardos 

Si desea probar si PHP puede establecer conexión con MySQL y ejecutar consultas a la BDD, podemos crear una tabla de prueba con datos ficticios y realizar consultas relacionadas con su contenido con una secuencia de comandos PHP. Para poder hacerlo, debemos crear una BDD de prueba y un usuario de MySQL nuevo debidamente configurado para acceder a ella.

De momento, la biblioteca PHP nativa de MySQL `mysqlnd` no [admite](https://www.php.net/manual/en/ref.pdo-mysql.php) `caching_sha2_authentication`, el método de autenticación predeterminado de MySQL8. Vamos a tener que crear un usuario nuevo con el método de autenticación `mysql_native_password` para poder establecer conexión con la BDD de MySQL desde PHP.

Crearemos una BDD denominada `example_database` y un usuario llamado `example_user`.

Primero, establece conexión con la consola de MySQL usando la cuenta `root`:

```bash
sudo mysql
```

Para crear una BDD nueva ejecutamos:

```sql
CREATE DATABASE example_database;
```

Ahora vamos a crear un usuario y concederle privilegios completos sobre la BDD personalizada que acabamos de crear. Elige una contraseña segura.

```sql
CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```

Ahora, le daremos permiso a este usuario sobre la BDD:

```sql
GRANT ALL ON example_database.* TO 'example_user'@'%';
```

Con esto, el usuario tendrá privilegios completos sobre la BDD y evitará que el usuario cree o modifique otras BDD de su servidor.

Cerramos el shell de MySQL:

```sql
exit
```

Podemos verificar si el usuario nuevo tiene los permisos adecuados al volver a iniciar sesión en la consola MySQL, esta vez con las credenciales de usuario personalizadas

```bash
sudo mysql -u example_user -p
```

El indicador `-p` en este comando, solicitará la contraseña que utilizó cuando creó el usuario. Vamos a comprobar que tenemos acceso a la BDD `example_database`

```sql
SHOW DATABASES;
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%207%20Probar%20la%20conexión%20con%20la%20BDD/Untitled.png)

Vamos a crear una tabla de prueba denominada todo_list: 

```sql
CREATE TABLE example_database.todo_list (
	item_id INT AUTO_INCREMENT,
	content VARCHAR(255),
	PRIMARY KEY(item_id)
);
```

Insertamos algunas filas de contenido en la tabla de prueba:

```sql
INSERT INTO example_database.todo_list (content) VALUES ("My first important item");
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%207%20Probar%20la%20conexión%20con%20la%20BDD/Untitled%201.png)

```sql
SELECT * FROM example_database.todo_list;
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%207%20Probar%20la%20conexión%20con%20la%20BDD/Untitled%202.png)

Después de confirmar que todo está bien, salimos de la consola de MySQL:

```sql
exit
```

Ahora vamos a crear una secuencia de comandos PHP que se conecte a MySQL y realice consultas relacionadas con su contenido. Creamos un fichero PHP en el directorio web root personalizado:

```bash
nano /var/www/prueba/todo_list.php
```

La siguiente secuencia de comandos PHP establece conexión con la BDD MySQL, realiza consultas relacionadas con el contenido de la tabla `todo_list` y muestra los resultados en una lista. Si hay problema con la conexión de la BDD genera una excepción. 

```php
<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```

![Captura de pantalla 2022-03-31 a las 13.21.45.png](Captura_de_pantalla_2022-03-31_a_las_13.21.45.png)

Guarda y cierra el archivo cuando finalices la edición `^x`, `y`, `Enter`

Ahora, si todo ha ido bien, podríamos acceder a nuestra página desde el browser:

`https://prueba.com/todo_list.php`