## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
```
C:\Users\ASUS TUF F15>docker network create net-wp
17b0d71701bd99a41b1fd0b0aff58647bd063d6981e45d5c8b770d9a1f49434c

C:\Users\ASUS TUF F15>docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
95994894f7c4   bridge    bridge    local
3e203dc59c57   host      host      local
17b0d71701bd   net-wp    bridge    local
08d55c19591d   none      null      local
```
### Para que persista la información es necesario conocer en dónde mysql almacena la información.
```
MySQL almacena sus datos en el directorio /var/lib/mysql dentro 
del contenedor.
```
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es (COMPLETAR CON LA RUTA)

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
```
La carpeta db del host inicialmente está vacía. Cuando se crea y ejecuta el contenedor MySQL con el bind mount a /var/lib/mysql, MySQL automáticamente 
inicializa la base de datos y genera todos los archivos necesarios en esta carpeta, incluyendo las bases de datos del sistema, archivos de datos, logs 
y configuraciones. Posteriormente contendrá todas las bases de datos creadas, como la de WordPress.
```
### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
C:\Users\ASUS TUF F15>docker run -d --name servidor-mysql --network net-wp -v "C:\Users\ASUS TUF F15\Desktop\Epn\6\Construcción de Software\ejercicio3\db":/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=wordpress_db -e MYSQL_USER=wordpress_user -e MYSQL_PASSWORD=wordpress_pass mysql:8
be34b888e734ec7629b51da9965f42e7db88e2a61a6f6d104d5c903a614515c4
```
### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
```
En la carpeta db que inicialmente estaba vacía, ahora se observan múltiples archivos y directorios creados automáticamente por MySQL. Se encuentran carpetas como mysql 
```
### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
```
Para que persista la información es necesario conocer en dónde wordpress almacena 
la información. WordPress almacena sus archivos en el directorio /var/www/html 
dentro del contenedor.
```

En el esquema del ejercicio la carpeta del contenedor (b) es (COMPLETAR CON LA RUTA)

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
C:\Users\ASUS TUF F15>docker run -d --name contenedor-wordpress --network net-wp -p 9500:80 -v "C:\Users\ASUS TUF F15\Desktop\Epn\6\Construcción de Software\ejercicio3\www":/var/www/html -e WORDPRESS_DB_HOST=servidor-mysql -e WORDPRESS_DB_USER=wordpress_user -e WORDPRESS_DB_PASSWORD=wordpress_pass -e WORDPRESS_DB_NAME=wordpress_db wordpress
195655b51971166210d331b19d27b753434d2f45176fced3f23a46bd7c725dc0
```
### Personalizar la apariencia de wordpress y agregar una entrada
<img width="1920" height="912" alt="imagen" src="https://github.com/user-attachments/assets/9e12bb32-d025-40e0-a89e-65bf93dadb5e" />

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
```
C:\Users\ASUS TUF F15>docker rm -f contenedor-wordpress
contenedor-wordpress
```
```
Al eliminar y volver a crear el contenedor de WordPress, me di cuenta que todo lo que había personalizado sigue ahí.
```
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 

