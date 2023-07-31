# Práctica 6: Probar el procesamiento de PHP en el servidor web

@Inma Gijón Cardos 

Vamos a crear una secuencia de comandos PHP de prueba para verificar que Apache pueda gestionar y procesar solicitudes de ficheros PHP.

```bash
nano /var/www/prueba/info.php #Con esto se crea un fichero vacío 
```

```php
<?php
phpInfo();
?>
```

Para probar la secuencia de archivos, en el browser, `https://prueba.com/info.php`

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%206%20Probar%20el%20procesamiento%20de%20PHP/Untitled.png)

Si puedes ver esta página en el navegador, tu configuración está **OK**.

Una vez comprobado, borramos dicho archivo, ya que contiene información confidencial sobre el entorno PHP y el servidor Ubuntu sobre el que estamos trabajando.

```bash
sudo rm /var/www/prueba/info.php
```