# Práctica 5: Instalar certificado SSL Let’s Encrypt en Apache

@Inma Gijón Cardos 

<aside>
💡 Vamos a instalar certificados SSL en un server apache a través de Let’s encrypt y utilizando certbot.

</aside>

<aside>
💡 Un certificado SSL es un **certificado** digital que autentica la identidad de un sitio web y habilita una conexión cifrada. La sigla **SSL** significa Secure Sockets Layer (Capa de sockets seguros), un protocolo de seguridad que crea un enlace cifrado entre un servidor web y un navegador web.

</aside>

- Debemos tener configurado Apache saliendo por HTTPS y el puerto 443 abierto.
- Tenemos que tener registrado un dominio pero como lo tenemos en local en modo de prueba configurado, nos sirve. También tendríamos que tener correctamente configurados los DNS del dominio registrado.
- Vamos a la página de `certbot`

[Certbot](https://certbot.eff.org/)

- Elegimos la configuración de nuestro sitio web y podemos obtener las instrucciones para realizar la instalación mediante `snapd` aunque no lo vamos a hacer así.

```bash
sudo apt install certbot python3-certbot-apache
sudo apache2ctl configtest #Comprueba la configuración del host
sudo systemctl reload apache2
sudo certbot --apache
```

- Nos indica dos preguntas: en primer lugar si estamos de acuerdo con las políticas de privacidad (le decimos que sí) y después si queremos compartir los datos con la organización (le decimos que no).
- Nos va a devolver un error porque no tenemos estos dominios registrados.
- Si sí los tuviésemos registrados obtendríamos algo así:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%205%20Instalar%20certificado%20SSL%20Let’s%20Encrypt/Untitled.png)

- Nos pregunta si queremos que salga por HTTP o HTTPS, lo adecuado es HTTPS.
- Después, nos indicaría lo siguiente: el certificado ha sido generado y dónde se encuentran los certificados que se quedan instalados automáticamente.

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%205%20Instalar%20certificado%20SSL%20Let’s%20Encrypt/Untitled%201.png)

- Let’s encrypt nos proporciona certificados SSL por un periodo de 90 días, después habría que renovarlos. Certbot deja corriendo un proceso que renueva automáticamente ese periodo, para verificarlo:

```bash
sudo systemctl status certbot.timer
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/3%20Configuración%20y%20administración%20de%20servidores%20w%2069e3a558938b461e9e0f9ef86ff72c7c/Práctica%205%20Instalar%20certificado%20SSL%20Let’s%20Encrypt/Untitled%202.png)

- Para probar el proceso de renovación podríamos hacer un simulacro con:

```bash
sudo certbot renew --dry-run
```

- Más información en:

[Cómo proteger Apache con Let's Encrypt en Ubuntu 20.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-20-04-es)

[Diferencias entre certificados SSL de pago y Let's Encrypt](https://blog.dondominio.com/diferencias-entre-certificados-ssl-de-pago-y-lets-encrypt/)