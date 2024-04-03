# Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad

## Índice

1. [Introducción](#Introducción)
2. [Configuración del balanceador web](#configuración-del-balanceador-web)
3. [Configuración del servidor web 1](#configuración-del-servidor-web-1)
4. [Configuración del servidor web 2](#configuración-del-servidor-web-2)
5. [Configuración del servidor NFS y el motor PHP](#configuración-del-servidor-NFS-y-el-motor-PHP)
6. [Configuración del servidor de datos](#configuración-del-servidor-de-datos)
7. [Conclusión](#conclusión)

# Introducción

En esta práctica implementaremos una intalación de wordpress en un estructura de cuatro capas, ya que esta estructura es más robusta y en la que se encuentran el la primera capa un balanceador de carga, en la segunda dos servidores backend  y un servidor nfs, en la tercera capa encontraremos un balanceador sql y en la cuarta y última capa encontraremos nuestros dos servidores de base de datos.

# Configuración del balanceador web

Para comenzar con nuestra configuración de nuestro balanceador web, tendremos que crear el fichero "load_balancer.conf" y posteriormente editarlo, dentro de este fichero tendremos que añadir la ip de los dos servidores que están como ya hemos explicado antes en la capa 2.

![editar fichero load_balancer conf](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/0698b8c6-e3bf-4d70-8322-b12d3124db46)

![image](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/01cee1b6-4949-4fa5-bf5c-28023d91ce0f)

Una vez hecho lo anterior podemos borrar en "/etc/nginx/sites-enabled" el fichero "default".
![image](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/7230f39d-f0b5-483b-832a-a9c6483300b4)

# Configuración del servidor web 1

Ahora vamos y una vez hayamos realizado el balanceador de carga pasaremos a configurar el servidor web 1. Para ello, empezaremos copiando el fichero "default" y en mi caso le he puesto "serverweb1", después he creado un enlace desde la ruta en la que se encuentra hasta "/etc/nginx/sites-enabled".

![Copiar default y enlace simbolico serverweb1](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/a851c13c-d46a-4b0f-964a-d2d454dbfb3f)

Una vez hecho esto, tendremos que editar el fichero en la línea "fastcgi_pass" hay que poner la ip del servidor nfs:9000;

![editar el fichero de sites-enable](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/3373b9e9-5dde-49e6-abfe-43e8a96c09d6)

Y debajo del DocumentRoot, hay que añadir index.php justo detrás de index.

![editar el fichero de sites-enable2](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/2ca2ac0f-965a-4cee-9c45-5c7527e0d250)

# Configuración del servidor web 2

Para nuestro servidor web 2, tendremos que realizar los mismos pasos que el servidor anterior.

![copiar configuracion default en serverweb2](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/74aeeb42-2d7a-4a05-8103-e7a6e24f0a48)

![editar el fichero de sites-enable](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/3373b9e9-5dde-49e6-abfe-43e8a96c09d6)

![editar fichero sites-enable en serverweb2](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/8a4b690c-f441-4ee7-a944-8fb0424277ef)

# Configuración del servidor NFS y el motor PHP

Para nuestro servidor NFS necesitamos editar el fichero "www.conf" que se encuentra en la siguiente ruta "/etc/php/7.3/pool.d/www.conf" y añadimos la siguiente línea.

![Modificar listen ](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/7c94eca8-6b07-4175-a0e1-3dd8c57398f7)

Reiniciamos el servicio.

![reiniciar el servicio](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/d1c253c8-0e49-45e6-9b21-6fda286b0ed7)

Ahora tendremos que descargar wordpress en los servidores web 1 y 2. En el servidor NFS también lo descargamos y creamos el directorio "/var/www/html"

![Descargar wordpress en servidorweb1](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/f46e9d22-9753-4639-8315-bc784b8973c6)

![Descomprimir archivo en serverweb1](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/2bd34fec-d3fd-4d4d-8a5d-bed04d4ad982)

Cambiamos el propietario y el grupo de la carpeta "wordpress" a "nobody nogroup".

![image](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/82664b74-a401-4d8e-944e-7ea41b5a1256)

Luego nos tendremos que ir al servidor nfs e introducir la siguiente linea.

![image](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/b9d5877a-0ad7-4ff2-8c3a-cb1029b95f93)

Comprobamos que está el servicio correctamente activo.

![image](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/48396f46-4a4d-41d1-b4ae-0e4078080600)

# Configuración del servidor de datos

El siguiente paso para nuestra configuración será realizar la configuración de nuestros servidores de base de datos, para los cuales realizaremos los siguientes pasos.

En primer lugar, tendremos que crear la base de datos, un usuario y darle permisos para que pueda acceder a ella.

![Crear base de datos y crear usuario](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/bdd5753c-0d5b-4ae6-94f1-cb1a5ddf29ed)

Después, tendremos que editar el DocumentRoot.

![editar el document root](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/d924f5c1-1dcd-4717-9216-c060cd7bbc46)

Por último, tendremos que irnos a nuestros servers web y editar el fichero wp-config.php

![cambiamos el nombre al fichero](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/342058de-ce87-4cb8-a2d2-08445cf7905d)

![editar fichero wp-config](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/143cdfb9-6ffc-4a90-a88f-c21978369979)

# Conclusión

Para esta práctica se ha implementado la estructura de capa 4 para que haya una mejor disponibilidad a la hora de algún posible fallo, por ejemplo si se cayese un servidor web o un servidor de datos y no se pierdan la productividad, ya que siempre habrá uno levantado por el que pasará el tráfico.
