# Instalación y configuración de entorno LAMP(Apache, php y MySql) en UBUNTU

## APACHE
- Instalación de apache:
  ```
  sudo apt install apache2
  ```
- Comprobación firewall

  ```
  sudo ufw app list
  ```

  - Se vería algo así

  ```
  Available applications:
    Apache
    Apache Full
    Apache Secure
    OpenSSH //Si se tiene activado el ssh
  ```

  - Explicación:
    - Apache: este perfil abre solo el puerto 80 (tráfico web normal no cifrado).
    - Apache Full: este perfil abre los puertos 80 (tráfico web normal no cifrado) y 443 (tráfico TLS/SSL cifrado).
    - Apache Secure: este perfil abre solo el puerto 443 (tráfico TLS/SSL cifrado).

- Al no tener configurado un certificado TLS/SSL permitimos unicamente tráfico en el puerto 80

```
sudo ufw allow in "Apache"
```

- Verificación status firewall

```
sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
Apache                     ALLOW       Anywhere
22/tcp (v6)                ALLOW       Anywhere (v6)
Apache (v6)                ALLOW       Anywhere (v6)
```
- Verificamos funcionamiento de servidor poniendo en el navegador la ip del mismo.
<hr>

## MY SQL:
- Instalación:
```
sudo apt install mysql-server
```
- Instalar y configturar seguridad:
```
sudo mysql_secure_installation
```
    -Se le preguntará si desea configurar el VALIDATE PASSWORD PLUGIN.

     Si se habilita, MySQL rechazará con un mensaje de error las contraseñas que no coincidan con los criterios especificados. Dejar la validación desactivada será una opción segura, pero siempre deberá utilizar contraseñas seguras y únicas para credenciales de bases de datos. No es obligatorio habilitarla



### POSIBLE ERROR DURANTE INSTALACIÓN
```
Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost' as the authentication method used doesn't store authentication data in the MySQL server. Please consider using ALTER USER instead if you want to change authentication parameters

```
- SOLUCIÓN:
    - Accede mediante otro terminal y cambia la contraseña del usuario root en este caso:
    ```
    sudo mysql
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'mynewpassword';
    ```
- Arrancar mysql
```
sudo systemctl start mysql
```
- Verifcicar estatus
```
sudo systemctl status mysql
```

<hr>

* Configuración de permisos para acceso remoto:
  - Configuramos el cortafuegos para permitir conexión:
```
  sudo ufw allow 3306
```
 - Modificamos el archivo "sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf"
    - En la línea "bind-address" especifica que la ip es la 127.0.0.1 esto quiere decir que solo admite conexiones locales, la cambiamos por la ip del server, por ejemplo "192.168.1.55"
    - Guardamosy cerramos
 - Reiniciamos servicio: "sudo systemctl restart mysql"

 - Permitir la conexión remota a un usuario de MySQL:
```
RENAME USER 'pym'@'localhost' TO 'pym'@'ip_servidor_remoto';
``` 


## Instalación y configuración de PHP
- Instalacion:
    - El paquete php, necesitará php-mysql, un módulo PHP que permite que este se comunique con bases de datos basadas en MySQL.
    - Instalamos apahce para la presentación del contenido
    ```
    sudo apt install php libapache2-mod-php php-mysql
    ```
    - Verificamos versión de php
    ```
    php -v
    PHP 8.1.2-1ubuntu2.9 (cli) (built: Oct 19 2022 14:58:09) (NTS)
    Copyright (c) The PHP Group
    Zend Engine v4.1.2, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.2-1ubuntu2.9, Copyright (c), by Zend Technologies

    ```

- Mostrer errores en php
  -Editamos el archivo php.ini en Ubuntu "/etc/php/versionphp/apache2/php.ini, y modficamos el valor display_errors poniéndolo así:
  ```
  display_errors = on
  ```


<hr>

## Configuración Apache

### Crear un host virtual para un sitio web:
- Creamos el directorio
```
sudo mkdir /var/www/dominio-prueba
```

- Asignamos la propiedad del directorio con la variable de entorno $USER, que hará referencia a su usuario de sistema actual:
```
sudo chown -R $USER:$USER /var/www/dominio-prueba
```

- Abrimos un archivo de configuración en "sites-available"
```
sudo nano /etc/apache2/sites-available/dominio-prueba.conf 
```
-Configuración básica que pegamos

    <VirtualHost *:80>
        ServerName dominio-prueba
        ServerAlias www.dominio-prueba
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/dominio-prueba
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>


NOTA:
Con esta configuración de VirtualHost, le indicamos a Apache que proporcione dominio-prueba usando /var/www/dominio-prueba como directorio root web. Si desea probar Apache sin un nombre de dominio, puede eliminar o convertir en comentario las opciones ServerName y ServerAlias añadiendo un carácter # al principio de las líneas de cada opción.


- Creamos un host virtual:
```
sudo a2ensite dominio-prueba
```

- Eliminar el sitio web por defecto que viene con Apache:
```
sudo a2dissite 000-default
```

- Verificar archivo de configuración
```
sudo apache2ctl configtest
```
- Recargamos Apache para que los cambios tengan efecto:
```
sudo systemctl reload apache2
```

- Crear un archivo para provar el host virtual
```
nano /var/www/dominio-prueba/index.html

<h1>Funcionando!</h1>

<p>Landing page de <strong>dominio-prueba</strong>.</p>
```

- Probar que este corriendo correctamente php en el server 
```
nano /var/www/dominio-prueba/info.php

<?php
phpinfo();

```
- Navegamos a la direccion IP