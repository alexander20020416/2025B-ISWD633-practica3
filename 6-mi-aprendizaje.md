# REFLEXIÓN DE APRENDIZAJES

Antes de realizar esta práctica, mi comprensión sobre volúmenes en Docker era bastante superficial. Sabía que existían y que se usaban para "guardar datos", pero no entendía realmente cómo funcionaban ni cuándo usar cada tipo. Ahora, después de completar todos los ejercicios, puedo decir que mi aprendizaje ha sido significativo y práctico.

**Lo que más me impactó fue entender las diferencias reales entre los tres tipos de volúmenes.** Al principio pensaba que todos eran lo mismo, pero trabajar con bind mounts me hizo ver que son perfectos cuando necesito editar archivos desde mi computadora y ver los cambios reflejados inmediatamente en el contenedor, como pasó con el template de HTML5UP en nginx. Fue genial ver cómo al copiar los archivos a mi carpeta local, automáticamente aparecían en el navegador sin tener que reconstruir nada.

Los volúmenes nombrados los entendí mejor con el ejercicio de Drupal y PostgreSQL. Me di cuenta de que son ideales cuando necesito que los datos persistan pero no necesito acceder directamente a ellos desde mi sistema operativo. **La clave está en que Docker los gestiona completamente**, lo cual simplifica mucho el manejo de bases de datos y configuraciones importantes. Cuando eliminé y volví a crear el contenedor de PostgreSQL usando el mismo volumen, ver que toda la configuración de la base de datos seguía ahí me hizo entender el verdadero valor de la persistencia.

En cuanto a los volúmenes anónimos, al principio me parecieron confusos porque no les das nombre. Pero después de usarlos entendí que son prácticos para datos temporales o cuando no planeo reutilizar ese volumen específicamente. **Lo importante que aprendí es acordarme del flag `-v` al eliminar contenedores**, porque si no, los volúmenes anónimos se quedan ahí ocupando espacio sin que te des cuenta.

**Un aprendizaje importante fue con el ejercicio de WordPress y MySQL.** Ver cómo dos contenedores se comunican a través de una red de Docker y cómo cada uno mantiene sus propios datos persistentes me ayudó a visualizar arquitecturas más complejas. Cuando personalicé WordPress, eliminé el contenedor y lo volví a crear, y todo seguía igual, ese momento fue como un "click" en mi cabeza sobre por qué la persistencia es tan crucial en aplicaciones reales.

También tuve que resolver algunos problemas que no estaban en la guía. Por ejemplo, cuando primero creé el contenedor de nginx con bind mount y me apareció el error 403 Forbidden, me quedé confundido unos minutos hasta que me di cuenta de que la carpeta html estaba vacía. Esto me enseñó a **siempre verificar el contenido de los directorios antes de montar volúmenes**.

Otro problema que encontré fue al trabajar con las rutas en Windows. Tuve que poner comillas dobles en las rutas porque tenían espacios, algo que no está muy claro en la documentación pero que es esencial: `"C:\Users\ASUS TUF F15\Desktop\..."`. Sin las comillas, Docker no reconocía la ruta correctamente.

**El diagrama de arquitectura que hice para Drupal me ayudó muchísimo a visualizar cómo todo se conecta.** Antes solo ejecutaba comandos sin entender bien la estructura completa, pero al tener que dibujar cómo la red conecta los contenedores, cómo cada volumen se monta en rutas específicas, y cómo los puertos permiten acceder desde el host, toda la arquitectura cobró sentido.

Para mi formación profesional, estos conocimientos son fundamentales porque ahora entiendo que **en ambientes de producción necesitas persistencia de datos confiable**. No puedes simplemente perder información cada vez que actualizas o reinicias un contenedor. Saber cuándo usar bind mounts (desarrollo), volúmenes nombrados (producción) o volúmenes anónimos (temporal) es una habilidad que definitivamente voy a usar en proyectos reales.

También aprendí a ser más cuidadoso con los comandos de eliminación. El `docker volume prune` es muy útil para limpiar, pero **hay que estar seguro de que no estás eliminando datos importantes**. Ver todos esos volúmenes anónimos acumulados me hizo consciente de la importancia de una buena gestión de recursos.

Finalmente, un aprendizaje inesperado fue la importancia de leer la documentación de cada imagen en Docker Hub. Cuando necesitaba saber dónde MySQL o WordPress guardaban sus datos, la documentación oficial me salvó. Antes trataba de adivinar o buscar en foros, pero ahora sé que **la fuente oficial siempre tiene la información correcta sobre los puntos de montaje recomendados**.

En resumen, pasé de tener un conocimiento teórico básico sobre volúmenes a poder implementarlos con confianza en diferentes escenarios. Entiendo sus diferencias, sus casos de uso, y lo más importante, cómo diseñar arquitecturas de contenedores que persistan datos de manera efectiva y segura.
