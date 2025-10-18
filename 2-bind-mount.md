# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
```
C:\Users\ASUS TUF F15>docker run -d --name mi-nginx -p 80:80 -v "C:\Users\ASUS TUF F15\Desktop\Epn\6\Construcción de Software\nginx\html":/usr/share/nginx/html nginx:alpine
efd8beb399030f18dcc855149afcc9ada0eb99545f30e2a53875376ac8e15b
```
### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
```
Al ingresar al servidor nginx (http:://localhost), aparece un error 403 Fobidden.
Esto sucede porque la carpeta html mapeada está vacía y nginx no encuentra un archivo index.html para servir.
```
### ¿Qué pasa con el archivo index.html del contenedor?
```
El archivo index.html original del contenedor queda oculto/reemplazado por el contenido de la carpeta del host debido al bind mount. El montaje hace que el 
directorio local tome prioridad sobre el directorio del contenedor, ocultando temporalmente los archivos originales sin eliminarlos de la imagen.
```
### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
```
Cuando entré a localhost apareció el template Story funcionando perfectamente, 
con todo su diseño y estilos. Se ve muy bien y todo carga correctamente. Gracias 
al bind mount, nginx está leyendo los archivos directo de mi carpeta, así que 
no tuve que hacer nada más después de copiar los archivos.
```
<img width="1920" height="912" alt="imagen" src="https://github.com/user-attachments/assets/718ed13f-c644-489a-ad4d-159b874d87ae" />

### Eliminar el contenedor
```
C:\Users\ASUS TUF F15>docker rm -f mi-nginx
mi-nginx
```
### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
```
Al crear nuevamente el contenedor con el mismo bind mount, todo vuelve a funcionar 
igual que antes. El template "Story" sigue ahí y se visualiza perfectamente en 
localhost. Esto pasa porque los archivos están guardados en mi computadora, no 
dentro del contenedor. Aunque eliminé el contenedor anterior, mis archivos nunca 
se borraron, así que el nuevo contenedor simplemente los vuelve a leer desde mi 
carpeta local.
```

