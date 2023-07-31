# Práctica 4: HTTPS en Apache Linux y redirección HTTP a HTTPS

@Inma Gijón Cardos 

<aside>
💡 HTTP no cifra el contenido entre el navegador y el servidor, para eso tenemos HTTPS que sí cifra la información entre el navegador.

</aside>

<aside>
💡 Si tenemos un sitio dinámico con BDD, lo recomendable es que salga por HTTPS y tenga los respectivos certificados SSL.

</aside>

- Vamos a habilitar HTTPS.
- Abrimos el terminal como `root`.

```bash
a2enmod ssl
systemctl restart apache2
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%204%20HTTPS%20en%20Apache%20Linux%20y%20redirección%20H%201b1a890ee57c4b2487b2e3e817abda45/Untitled.png)

```bash
cd /etc/apache2/sites-available
ls
cat default-ssl.conf
```

- Vemos que tenemos además de los ficheros de `conf` que trabajamos en la práctica anterior, el fichero `default-ssl.conf`
- Podemos ver que es el sitio por defecto de apache pero que sale por el puerto `443` y está en https, con opciones como `SSLEngine on` y dos ficheros `SSLCertificateFile` y `SSLCertificateKeyFile`
- Lo que vamos a hacer es copiar el contenido de `default-ssl.conf` y pegarlo en `prueba.conf` a continuación de lo que teníamos quedando lo siguiente (quitando los comentarios). También hemos cambiado el `*` por el nombre del sitio `prueba.com`y algunos cambios más como podemos ver:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%204%20HTTPS%20en%20Apache%20Linux%20y%20redirección%20H%201b1a890ee57c4b2487b2e3e817abda45/Untitled%201.png)

<aside>
💡 Tenemos que asegurarnos de que el puerto está abierto en el cortafuegos (443 es el de por defecto de HTTPS)

</aside>

```bash
systemctl restart apache2
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%204%20HTTPS%20en%20Apache%20Linux%20y%20redirección%20H%201b1a890ee57c4b2487b2e3e817abda45/Untitled%202.png)

<aside>
💡 No están instalados los certificados y nos indica que es un sitio inseguro.

</aside>

- La configuración por HTTP sigue siendo funcional y podríamos seguir accediendo pero no es lo recomendable, por eso en `prueba.conf` hemos puesto `Redirect / https://prueba.com`