## VOLUMEN NOMBRADO
Un volumen nombrado (named volume) es un tipo de volumen gestionado por Docker que se almacena en una ubicación específica del sistema de archivos del host y se identifica mediante un nombre único. Los volúmenes nombrados no requieren que especifiques una ruta del sistema de archivos del host, y en su lugar, Docker se encarga de la gestión y el almacenamiento del volumen.


### Crear volumen
```
docker volume create <nombre volumen>
```

### Crear el volumen nombrado: vol-postgres
```
C:\Users\ASUS TUF F15>docker volume create vol-postgres
vol-postgres
```
## MOUNTPOINT
Un mountpoint se refiere al lugar en el sistema de archivos donde un dispositivo de almacenamiento se une (o monta) al sistema de archivos. Es el punto donde los archivos y directorios almacenados en ese dispositivo de almacenamiento son accesibles para el sistema operativo y las aplicaciones.

Por ejemplo, en Windows las unidades de almacenamiento (como `C:`, `D:`, etc.) actúan como puntos de montaje principales para discos duros, unidades flash, unidades ópticas y otros dispositivos de almacenamiento.

Cuando creas un volumen nombrado, Docker asigna un punto de montaje específico en el sistema de archivos del host para ese volumen.

### Estructura del Punto de Montaje:
- /var/lib/docker/volumes/: Es la ubicación base donde Docker almacena todos los volúmenes en el sistema de archivos del host.
- nombreVolumen/: Es el nombre del volumen nombrado que has creado. Docker crea un directorio con este nombre dentro de /var/lib/docker/volumes/ para almacenar los datos del volumen.
- _data: Es el subdirectorio dentro de vol-postgres/ donde se almacenan los datos reales del volumen. El nombre _data es una convención utilizada por Docker para indicar el directorio donde se encuentran los datos del volumen.

### ¿Cómo acceder a ese Mountpoint?
En el contexto de WSL (Windows Subsystem for Linux), wsl$ se refiere al nombre de un recurso compartido de red especial que representa la raíz del sistema de archivos de Windows desde WSL. Cuando accedes a \\wsl$ desde el Explorador de archivos de Windows, puedes ver y acceder a los archivos del sistema de archivos de la distribución de Linux en WSL.
\\wsl.localhost\docker-desktop-data\data\docker\volumes

### Crear un contenedor vinculado a un volumen nombrado
```
docker run -d --name <nombre contenedor> -v <nombre volumen>:<ruta contenedor> <nombre imagen>
```
ó
```
docker run -d --name <nombre contenedor> --mount type=volume,src=<nombre >,dst=<mount-path>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje. Para volúmenes con nombre, este es el nombre del volumen. Para volúmenes anónimos, este campo se omite.


### Crear la red net-drupal de tipo bridge
```
C:\Users\ASUS TUF F15>docker network create --driver bridge net-drupal
eb19ba0463af57130b188ec67ebed4ae1cfc37dd659353b5bbee7443e2295482

C:\Users\ASUS TUF F15>docker network ls
NETWORK ID     NAME         DRIVER    SCOPE
9536ed69a613   bridge       bridge    local
3e203dc59c57   host         host      local
eb19ba0463af   net-drupal   bridge    local
08d55c19591d   none         null      local
```
### Crear un servidor postgres vinculado a la red net-drupal, completar la ruta del contenedor
```
docker run -d --name server-postgres -e POSTGRES_DB=db_drupal -e POSTGRES_PASSWORD=12345 -e POSTGRES_USER=user_drupal --network net-drupal postgres
```
_No es necesario exponer el puerto, debido a que nos vamos a conectar desde la misma red de docker_
```
C:\Users\ASUS TUF F15>docker run -d --name server-postgres -e POSTGRES_DB=db_drupal -e POSTGRES_PASSWORD=12345 -e POSTGRES_USER=user_drupal -v vol-postgres:/var/lib/postgresql/data --network net-drupal postgres
Unable to find image 'postgres:latest' locally
latest: Pulling from library/postgres
af60ce4418c9: Pull complete
751039babae5: Pull complete
f0d70120d9e2: Pull complete
f69a7c424b50: Pull complete
eed0ac863490: Pull complete
dd6d7b9d8ba8: Pull complete
1014e14b3351: Pull complete
2433c366ca00: Pull complete
f5af7533693a: Pull complete
203b16f56a7d: Pull complete
edd90ab5059f: Pull complete
a585c5f82f15: Pull complete
9a68d6020eab: Pull complete
Digest: sha256:073e7c8b84e2197f94c8083634640ab37105effe1bc853ca4d5fbece3219b0e8
Status: Downloaded newer image for postgres:latest
d784518f6f705446ea973382d85abf2c139072cf126264206fb16298d7fbc3f2

C:\Users\ASUS TUF F15>docker ps -a
CONTAINER ID   IMAGE      COMMAND                  CREATED          STATUS          PORTS      NAMES
d784518f6f70   postgres   "docker-entrypoint.s…"   31 seconds ago   Up 30 seconds   5432/tcp   server-postgres
```
### Crear un cliente postgres vinculado a la red drupal a partir de la imagen dpage/pgadmin4, completar el correo
```
docker run -d --name client-postgres --publish published=9500,target=80 -e PGADMIN_DEFAULT_PASSWORD=54321 -e PGADMIN_DEFAULT_EMAIL=<correo> --network net-drupal dpage/pgadmin4
```
```
C:\Users\ASUS TUF F15>docker run -d --name client-postgres --publish published=9500,target=80 -e PGADMIN_DEFAULT_PASSWORD=54321 -e PGADMIN_DEFAULT_EMAIL=admin@admin.com --network net-drupal dpage/pgadmin4
7dd763bf38f374f5f474a4543a4bda01c88f9521e06f758f7129b5e600e4ebd0
```
### Usar el cliente postgres para conectarse al servidor postgres, para la conexión usar el nombre del servidor en lugar de la dirección IP.

### Crear los volúmenes necesarios para drupal, esto se puede encontrar en la documentación
### COMPLETAR CON LOS COMANDOS

### Crear el contenedor server-drupal vinculado a la red, usar la imagen drupal, y vincularlo a los volúmenes nombrados
```
docker run -d --name server-drupal --publish published=9700,target=80 -v <nombre volumen>:<ruta contenedor> -v <nombre volumen>:<ruta contenedor> -v <nombre volumen>:<ruta contenedor> -v <nombre volumen>:<ruta contenedor> --network net-drupal drupal
```

### Ingrese al server-drupal y siga el paso a paso para la instalación.
# COMPLETAR CON UNA CAPTURA DE PANTALLA DEL PASO 4
<img width="1305" height="1447" alt="imagen" src="https://github.com/user-attachments/assets/45396bfc-cb04-4aef-93aa-1c4e189a1fc2" />

_La instalación puede tomar varios minutos, mientras espera realice un diagrama de los contenedores que ha creado en este apartado._

# COMPLETAR CON EL DIAGRAMA SOLICITADO
<img width="1918" height="2745" alt="imagen" src="https://github.com/user-attachments/assets/3107cd24-875b-4f6b-9ce7-e5ab3eb67ac8" />

<img width="903" height="448" alt="imagen" src="https://github.com/user-attachments/assets/3ee8ff13-b9b0-4a61-88a2-d5f5451952e3" />

### Eliminar un volumen específico
```
docker volume rm <nombre volumen>
```
```
C:\Users\ASUS TUF F15>docker stop server-postgres
server-postgres

C:\Users\ASUS TUF F15>docker rm server-postgres
server-postgres

C:\Users\ASUS TUF F15>docker volume rm vol-postgres
vol-postgres
```
**Considerar**
Datos Persistentes: Asegúrate de que el volumen no contiene datos críticos antes de eliminarlo, ya que esta operación no se puede deshacer.
Contenedores Activos: No puedes eliminar un volumen que está actualmente en uso por un contenedor activo. Debes detener y/o eliminar el contenedor primero.
