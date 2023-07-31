# Práctica 1: Instalación y configuración básica de Apache

@Inma Gijón Cardos 

<aside>
💡 Vamos a instalar Apache sobre [Ubuntu 20.04 LTS](https://ubuntu.com/download/desktop) que podemos virtualizar mediante [VirtualBox](https://www.virtualbox.org/).

</aside>

<aside>
💡 Instalar Guest Additions

</aside>

# Pasos a seguir

- Debemos estar logueados como **`root`** y actualizamos el sistema

```bash
sudo su
```

```bash
apt update
```

- Después pasamos a instalar apache

```bash
apt install apache2
```

- Una vez que termine, vamos a verificar que esté funcionando correctamente. Para ello abrimos el navegador y comprobamos introduciendo: [http://localhost](https://www.youtube.com/playlist?list=PLcgWA1YrA0ID_VrCmeCWNbUD3tsdAo3eW)
- En la página aparece información sobre datos de configuración básicos de Apache.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled.png)

<aside>
💡 Si no funciona puede ser: problemas con un firewall habilitado o problemas con iptables comprobamos con los comandos siguientes

</aside>

```bash
ufw status
```

```bash
iptables -L
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%201.png)

- Toda la configuración de apache se encuentra en `/etc/apache2`

```bash
cd /etc/apache2
ls -l
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%202.png)

- En `sites-available` veremos todos los sitios disponibles y en `sites-enabled`, todos los que están habilitados para mostrarse.

```bash
cd sites-available
cat 000-default.conf
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%203.png)

- Vemos que sale por el puerto 80
- ServerAdmin es el mail que estamos configurando
- DocumentRoot nos indica la ruta principal de ese sitio `/var/www/html`

```bash
cd /var/www/html
ls
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%204.png)

- Dicho index.html es lo que se mostraba cuando ingresamos en el navegador.
- Si creo un sitio nuevo un nivel por arriba sin ni siquiera etiquetas (lo vamos a crear con el editor nano) (`^X` para salir y guardar):

```bash
cd ..
nano index.html
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%205.png)

- Si hacemos http://localhost, vemos lo mismo que veíamos antes.

```bash
cd /etc/apache2/sites-enabled
ls
nano 000-default.conf
```

- Si editamos la configuración y pongo en la línea en la que aparece:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%206.png)

- Para que se aplique el cambio hay que hacer un `reload`:

```bash
systemctl reload apache2
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%207.png)

- Para comprobar si está funcionando correctamente:

```bash
systemctl status apache2
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%208.png)

- Si queremos parar el servicio:

```bash
systemctl stop apache2
systemctl status apache2
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%209.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%201%20Instalación%20y%20configuración%20básica/Untitled%2010.png)

- Para iniciarlo de nuevo:

```bash
systemctl start apache2
```