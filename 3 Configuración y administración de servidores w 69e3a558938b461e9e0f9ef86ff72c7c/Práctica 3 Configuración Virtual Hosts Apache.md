# Práctica 3: Configuración Virtual Hosts Apache

@Inma Gijón Cardos 

---

- Vamos a ver cómo tener varios dominios sin tener la necesidad de tener distintos server.
- Vamos a crear las dos carpetas para el contenido de los diferentes sitios

```bash
sudo mkdir -p /var/www/prueba
sudo mkdir -p /var/www/prueba2
```

- Si vemos los permisos de esas carpetas, el propietario es el `root`:

```bash
cd /var/www
ls -l
```

- Si queremos que las carpetas tengan como usuario propietario un usuario que no sea `root`, hacemos:

```bash
sudo chown -R inmagijon:inmagijon prueba
sudo chown -R inmagijon:inmagijon prueba2
ls -l
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled.png)

- A la vez, a estas carpetas les daremos permisos:

```bash
sudo chmod 755 -R prueba
sudo chmod 755 -R prueba2
ls -l
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%201.png)

- Ahora vamos a ver la configuración por defecto:

```bash
cd /etc/apache2/sites-available
ls
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%202.png)

- Vamos a usar el `000-default.conf` como referencia para crear el resto:

```bash
sudo cp 000-default.conf prueba.conf
sudo nano prueba.conf
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%203.png)

- Vamos a hacer lo mismo para prueba2:

```bash
sudo cp prueba.conf prueba2.conf
sudo nano prueba2.conf
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%204.png)

- Estos sitios aún no están habilitados, deben estar en la carpeta `sites-enabled`.

```bash
sudo a2ensite prueba.conf
sudo a2ensite prueba2.conf
sudo systemctl reload apache2
```

- Si quiero abrir mis sitios, en primer lugar, en las carpetas vamos a crear `index.html`

```bash
cd /var/www/prueba
nano index.html
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%205.png)

```bash
cd /var/www/prueba2
nano index.html
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%206.png)

- Estos dominios no están registrados, son de prueba. Para que fuesen públicos deberíamos de tener nuestros DNS registrados ser públicos. Vamos a probar en local, configurando los DNS en local.
- Si hacemos `ip a` vemos loopback que es nuestro propio equipo luego la ip de red:

```bash
ip a
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%207.png)

```bash
sudo nano /etc/hosts
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%208.png)

```bash
sudo systemctl reload apache2
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%209.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%203%20Configuración%20Virtual%20Hosts%20Apache/Untitled%2010.png)

- Ya tenemos dos sitios creados con dos dominios en un mismo servidor.