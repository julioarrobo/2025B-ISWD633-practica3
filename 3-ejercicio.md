## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
# COMPLETAR CON EL COMANDO COMANDO
docker network create net-wp


### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es (/var/lib/mysql)

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Se llena con los archivos de datos de MySQL: directorios como mysql/, performance_schema/, sys/ y la carpeta de la BD wordpress/, además de ficheros InnoDB (por ejemplo ibdata*, ib_logfile*). Antes estaba vacía y ahora contiene toda la data del servidor.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
# COMPLETAR CON EL COMANDO
docker run -d --name mysql-wp --network net-wp --mount type=bind,source="C:\Users\JulioAPC\CONSTRUCCION\ejercicio3\db",target=/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpass -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppass mysql:8

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Al iniciar el contenedor de MySQL, la carpeta db del host, que inicialmente estaba vacía, se llena automáticamente con los archivos y directorios del sistema de base de datos.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es (/var/www/html)

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
docker run -d --name wordpress-wp -p 9500:80 --network net-wp --mount type=bind,source="C:\Users\JulioAPC\CONSTRUCCION\ejercicio3\www",target=/var/www/html -e WORDPRESS_DB_HOST=mysql-wp:3306 -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppass -e WORDPRESS_DB_NAME=wordpress wordpress:latest


### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
Al eliminar y volver a crear el contenedor de WordPress, el sitio web conserva toda su información (entradas, temas, configuraciones y archivos).
Esto ocurre porque los datos se guardan en carpetas del host mediante bind mounts:

La carpeta www contiene los archivos del sitio (temas, plugins, medios).

La carpeta db contiene la base de datos de MySQL con toda la información dinámica del sitio.

Por tanto, aunque el contenedor se elimine y se vuelva a crear, el contenido persiste sin pérdida de dato
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 

