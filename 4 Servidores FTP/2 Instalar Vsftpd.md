# 2. Instalar Vsftpd

#vsftpd 


```bash
sudo apt update
sudo apt install vsftpd
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.original #hacemos una copia de seguridad del archivo original
```

Habilitamos el puerto para el tráfico FTP desde el firewall si lo tenemos activo.

Para ver cómo habilitar y configurar el firewall de Ubuntu:

[Como Habilitar y Configurar el Firewall UFW en Ubuntu](https://computernewage.com/2014/08/10/como-configurar-el-firewall-ufw-en-ubuntu/#habilitar-ufw)

```bash
sudo ufw enable
sudo ufw allow 20/tcp
sudo ufw allow 21/tcp
sudo ufw allow 22/tcp
sudo ufw allow 990/tcp
sudo ufw allow 40000:50000/tcp
sudo ufw status
```

Debemos asegurarnos de tener habilitadas las reglas. Hemos habilitado los puertos específicos para que funcione correctamente nuestro servidor FTP.

```bash
sudo ufw allow in "Apache Full"
```

# Configuramos vsftpd.conf

```bash
sudo nano /etc/vsftpd.conf
```

Habilitaremos la escritura descomentándolo y habilitaremos `local_enable` también.

También buscaremos que `chroot` esté descomentado. De esta manera el usuario conectado por FTP lo limitaremos a que sólo acceda a los archivos de la carpeta permitida:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/2%20Instalar%20Vsftpd/Untitled.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/2%20Instalar%20Vsftpd/Untitled%201.png)

```bash
sudo service vsftpd restart #reiniciamos
sudo service vsftpd status
```

# Configuramos la seguridad del FTP

Creamos un certificado SSL:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.key -out /etc/ssl/certs/vsftpd.pem
```

Rellenamos lo que nos pide

Al finalizar abrimos:

```bash
sudo nano /etc/vsftpd.conf
```

Nos desplazamos al final del archivo y nos tiene que quedar así. Añadiremos las rutas del certificado y configuraremos datos relativos a SSL y TLS

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/2%20Instalar%20Vsftpd/Untitled%202.png)

Reiniciamos el servidor

```bash
sudo systemctl restart vsftpd
```

Obtenemos la ip de nuestro servidor con `ifconfig`

# Accedemos al servidor ftp

Para acceder a nuestro servidor ftp, es necesario tener instalado en nuestro equipo un cliente ftp como [FileZilla](https://filezilla-project.org/).

Lo instalamos, abrimos FileZilla y nos dirigimos al menú `Gestor de Sitios`, creamos un nuevo sitio:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/2%20Instalar%20Vsftpd/Untitled%203.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/2%20Instalar%20Vsftpd/Untitled%204.png)

El usuario y contraseña son los mismos que utilizamos para conectarnos por ssh.

Al darle a **conectar,** nos dirá que si queremos confiar en el servidor.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/2%20Instalar%20Vsftpd/Untitled%205.png)

Una vez dicho esto, nos mostrará el árbol de archivos de nuestra máquina:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/2%20Instalar%20Vsftpd/Untitled%206.png)