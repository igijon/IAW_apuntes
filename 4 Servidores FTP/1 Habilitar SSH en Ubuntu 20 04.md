
#ssh #ubuntu

# 1. Habilitar SSH en Ubuntu 20.04

Una vez que tenemos en el sistema **Ubuntu 20.04, Apache, MySQL y PHP**, vamos a habilitar la conexión **SSH**.

Secure Shell (SSH) es un protocolo de red que se utiliza para una conexión segura entre un cliente y un servidor. Cada interacción entre el servidor y el cliente está encriptada.

Habilitar SSH permitirá conectarnos al sistema de forma remota y realizar tareas administrativas. También permitirá transferir archivos de forma segura a través de `scp` y `sftp`.

**SCP** (Protocolo de copia segura) y **SFTP** (Protocolo de transferencia segura de archivos) son alternativas para **FTP** (Protocolo de transferencia de archivos), que resulta útil para las transferencias de archivos locales no programadas. Los tres pueden ayudar a lograr mover archivos de una ubicación a otra a través de Ethernet. Sin embargo, FTP envía los datos en texto plano, mientras que los otros dos utilizan el protocolo Secure Shell (SSH) para la comunicación.

```bash
sudo apt update
sudo apt install openssh-server
```

Una vez instalado, el servicio SSH se iniciará automáticamente. Verificamos:

```bash
sudo systemctl status ssh
```

Si tenemos el firewall habilitado en el sistema, tenemos que abrir el puerto SSH:

```bash
sudo ufw allow ssh
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/1%20Habilitar%20SSH%20en%20Ubuntu%2020%2004/Untitled.png)

Ahora podemos conectarnos a nuestro sistema Ubuntu desde cualquier máquina remota por SSH. Los sistemas Linux y macOS tienen clientes SSH instalados de forma predeterminada. Si tienes problemas para conectarte desde una máquina con Windows, puedes usar un cliente SSH como [PuTTY](https://www.putty.org/).

Para conectarnos:

```bash
ssh username@ip_address #ssh inmagijon@192.168.210.20. Puedes ver la ip con ifconfig
```

Si aparece este error:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/1%20Habilitar%20SSH%20en%20Ubuntu%2020%2004/Untitled%201.png)

Debemos corregir la clave del host en el directorio de host conocidos mediante:

```bash
ssh-keygen -R ip_server
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/4%20Servidores%20FTP/1%20Habilitar%20SSH%20en%20Ubuntu%2020%2004/Untitled%202.png)