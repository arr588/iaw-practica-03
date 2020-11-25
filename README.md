# iaw-practica-03

## Arquitectura de una aplicación web LAMP en dos niveles

### Configuración del front-end

El front-end va a ser quien aloje el servidor Apache, php junto a phpMyAdmin y todas las herramientas de gestión de la web, como adminer. En el va a ir implementado la web sin la base
de datos. Para ello he usado el script ya hecho en las prácticas anteriores añadiendo el código necesario para que conecte con la base de datos alojada en el back-end:

- Agregamos una variable para la IP privada de la máquina back-end

    `IP=172.31.86.55`

- Después de instalar phpMyAdmin modificamos el archivo config.inc.php para poner la IP privada del back-end

    `cp config.inc.php /var/www/html/phpmyadmin/`

    En este caso he optado por copiar el archivo completo pero se podría hacer sin un archivo extra con el comando sed.

- En la configuración de php cambiamos la IP de la base de datos a la de la máquina back-end

    `sed -i "s/localhost/$IP/" /var/www/html/config.php`

- Para acabar a la hora de instalar la aplicación web borramos la base de datos para no tener problemas

    `rm -rfv $DIR_GIT/db`

### Configuración del back-end

El back-end va a ser quien aloje la base de datos y los usuarios de MySQL que tienen acceso. Usamos la parte de MySQL del script anterior añadiendo:

- Cambiamos la IP del archivo de configuración de MySQL

    `sed -i "s/127.0.0.1/0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf`

- Para acabar a la hora de instalar la aplicación web borramos la carpeta src para no tener problemas

    `rm -rfv $DIR_GIT/src`