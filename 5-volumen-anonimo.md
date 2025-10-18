## VOLUMEN ANÓNIMO
Un volumen anónimo es un volumen gestionado por Docker, el volumen se crea automáticamente sin un nombre específico cuando ejecutas un contenedor. Son útiles cuando deseas almacenar datos temporalmente sin preocuparte por el nombre del volumen. Docker asigna un identificador único en lugar de un nombre. Se utilizan principalmente para almacenamiento temporal. 
**Considerar**
Los datos persisten mientras el contenedor exista, pero son más difíciles de gestionar y referenciar después.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta contenedor> <nombre imagen>
```
ó
```
docker run -d --name <nombre contenedor> --mount type=volume,target=<ruta carpeta contenedor> <nombre_imagen>
```
destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
```
C:\Users\ASUS TUF F15>docker run -d --name mi-nginx -v /usr/share/nginx/html nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
250b90fb2b9a: Pull complete
8da8ed3552af: Pull complete
54e822d8ee0c: Pull complete
5d8ea9f4c626: Pull complete
58d144c4badd: Pull complete
b459da543435: Pull complete
Digest: sha256:3b7732505933ca591ce4a6d860cb713ad96a3176b82f7979a8dfa9973486a0d6
Status: Downloaded newer image for nginx:latest
7e71fa6746fc207fc095f1c7fdf0129fa11d92f22413aa3ea5322c15a8939327
```
### Para eliminar el contenedor y el volumen
```
docker rm -fv server-nginx
```
_esta instrucción elimina el volumen si éste es de tipo anónimo_

# Eliminar todos los volúmenes anónimos (dangling volumes) no utilizados
Los dangling volumes son volúmenes en Docker que no están asociados a ningún contenedor en ejecución. Estos volúmenes se crean cuando se monta un volumen en un contenedor y luego se elimina ese contenedor sin eliminar explícitamente el volumen.
```
docker volume prune
```
```
C:\Users\ASUS TUF F15>docker rm -fv mi-nginx
mi-nginx
```
