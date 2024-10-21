# Práctica 2.3 – Proxy Inverso con Nginx

### Jaime Grueso Martin

## Indice
1. [Configuraciones](#id1)
    1. [Nginx Servidor Web](#id11)
    2. [Nginx Proxy Inverso](#id12)
2. [Comprobaciones](#id2)
    1. [Añadiendo Cabeceras](#id3)

<div id='id1'></div>

## Confifuraciones

<div id='id11'></div>

### Nginx Servidor Web
Primeramente se debe cambiar el nombre de la web a `webserver`, lo que implica que se deba cambiar el nombre
del sitio web dentro del archivo de configuración y finalmente eliminar el enlace simbolico previo y crear uno nuevo 
con el nombre del archivo.

![img](/docs/assets/images/screenshot.1.jpg)

El cual se editará de la siguinte manera y se le cambiará el puerto de escucha al 8080

![img](/docs/assets/images/screenshot.19.jpg)

Como se cambió de nombre el directorio, al ejecutar el comando `unlink`, se eliminará el archivo con `sudo rm -r`

![img](/docs/assets/images/screenshot.16.jpg)

Se creará el nuevo enlace simbolico y se reiniciará el servicio para que se apliquen los cambios

![img](/docs/assets/images/screenshot.17.jpg)

<div id='id12'></div>

### Nginx Proxy Inverso

A su vez, se creará un archivo en la máquina donde hayamos decidido crear el proxy en la ruta `/etc/nginx/sites-available/ejemplo-proxy`

![img](/docs/assets/images/screenshot.20.jpg)

El cual es más simple de editar ya que no tiene tanto contenido como el de `webserver`. Se indicará el pueto de escucha, el nombre del dominio modificado previamente, el `proxy-pass` que será a donde se redirijan las peticiones, por lo que habrá que poner la ip de la máquina que se esté utilizando como `webserver`

![img](/docs/assets/images/screenshot.8.jpg)

Se creará un enlace simbólico para este archivo.

![img](/docs/assets/images/screenshot.22.jpg)

A continuación se procederá a modificar el archivo `hosts` de la maquina anfitriona para que la ip coincida con la de la maquina de `webserver`

![img](/docs/assets/images/screenshot.21.jpg)


Ahora, cuando se intente acceder a `http://www.ejemplo-proxy.com`, se estará accediendo al proxy, que se redirigirá a `webserver`

![img](/docs/assets/images/screenshot.11.jpg)

<div id='id2'></div>

## Comprobaciones

Si se accede a la web se podrá ver en los access.log que están llegando las peticiones correspondientes

![img](/docs/assets/images/screenshot.24.jpg)

![img](/docs/assets/images/screenshot.25.jpg)

Y si se hace uso de las herramientas de desarrollador de Firefox. Pulsando F12 en el navegador os aparecerán unas herramientas. Se buscará la herramienta de `Red` y se activará la opción de desactivar la caché.

![img](/docs/assets/images/screenshot.26.jpg)

<div id='id21'></div>

### Añadiendo Cabeceras
Se va a configurar tanto el proxy inverso como el servidor web para que añadan cada uno la cabecera “Host”.

Se deberá añadir primeramente la cabecera al archivo de configuracion del proxy inverso de la siguiente manera.

![img](/docs/assets/images/screenshot.27.jpg)

Se reiniciará el servicio Nginx y se comprobará que en el buscador con la herramienta de Red, aparezca el nombre que se le ha asignado.

![img](/docs/assets/images/screenshot.28.jpg)

Ahora se procederá a hacerlo para el servidor web. El proceso es el mismo que para el proxy inverso.

![img](/docs/assets/images/screenshot.13.jpg)

Para este proceso se han modificado sos archivos mas, el archivo hosts de la máquina anfitriona y el archivo hosts de la máquina donde esta configurado el proxy inverso.

![img](/docs/assets/images/screenshot.15.jpg)

![img](/docs/assets/images/screenshot.23.jpg)

## Autor: Jaime Grueso Martin