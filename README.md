# Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad

##Índice


Introducción

En esta práctica implementaremos una intalación de wordpress en un estructura de cuatro capas, ya que esta estructura es más robusta y en la que se encuentran el la primera capa un balanceador de carga, en la segunda dos servidores backend  y un servidor nfs, en la tercera capa encontraremos un balanceador sql y en la cuarta y última capa encontraremos nuestros dos servidores de base de datos.

Configuración del balanceador web

Para comenzar con nuestra configuración de nuestro balanceador web, tendremos que crear el fichero "load_balancer.conf" y posteriormente editarlo, dentro de este fichero tendremos que añadir la ip de los dos servidores que están como ya hemos explicado antes en la capa 2.

![editar fichero load_balancer conf](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/0698b8c6-e3bf-4d70-8322-b12d3124db46)

Una vez hecho lo anterior podemos borrar en "/etc/nginx/sites-enabled" el fichero "default".
![borrar default en sites-enabled](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/13120c51-e637-4dd7-8b40-94640175bd07)

Configuración del servidor web 1

Ahora vamos y una vez hayamos realizado el balanceador de carga pasaremos a configurar el servidor web 1. Para ello, empezaremos copiando el fichero "default" y en mi caso le he puesto "serverweb1", después he creado un enlace desde la ruta en la que se encuentra hasta "/etc/nginx/sites-enabled".

![Copiar default y enlace simbolico serverweb1](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/a851c13c-d46a-4b0f-964a-d2d454dbfb3f)


Una vez hecho esto, tendremos que editar el fichero en la línea "fastcgi_pass" hay que poner la ip del servidor nfs:9000;

![editar el fichero de sites-enable](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/3373b9e9-5dde-49e6-abfe-43e8a96c09d6)

Y debajo del DocumentRoot, hay que añadir index.php justo detrás de index.

![editar el fichero de sites-enable2](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/2ca2ac0f-965a-4cee-9c45-5c7527e0d250)

Configuración del servidor web 2

Para nuestro servidor web 2, tendremos que realizar los mismos pasos que el servidor anterior.

![copiar configuracion default en serverweb2](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/74aeeb42-2d7a-4a05-8103-e7a6e24f0a48)

![editar el fichero de sites-enable](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/3373b9e9-5dde-49e6-abfe-43e8a96c09d6)

![editar fichero sites-enable en serverweb2](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/8a4b690c-f441-4ee7-a944-8fb0424277ef)

Configuración del servidor NFS y el motor PHP

Para nuestro servidor NFS necesitamos editar el fichero "www.conf" que se encuentra en la siguiente ruta "/etc/php/7.3/pool.d/www.conf" y añadimos la siguiente línea.

![Modificar listen ](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/7c94eca8-6b07-4175-a0e1-3dd8c57398f7)

Reiniciamos el servicio.

![reiniciar el servicio](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/d1c253c8-0e49-45e6-9b21-6fda286b0ed7)

Ahora tendremos que descargar wordpress en los servidores web 1 y 2. En el servidor NFS también lo descargamos y creamos el directorio "/var/www/html"

![Descargar wordpress en servidorweb1](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/f46e9d22-9753-4639-8315-bc784b8973c6)

![Descomprimir archivo en serverweb1](https://github.com/colival03/Cristian-Instalaci-n-de-Wordpress-en-alta-disponibilidad/assets/146434716/2bd34fec-d3fd-4d4d-8a5d-bed04d4ad982)

Configuración del servidor de datos

