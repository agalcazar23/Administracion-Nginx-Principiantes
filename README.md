# Administracion de Nginx para Principiantes 🐧

![nginx](nginx.jpeg)

A menudo, el Administrador de Sistemas recibe solicitudes para desplegar webs temporales por parte de otros departamentos. Para ello, es necesaria la creación de dominios en Nginx, la gestión de permisos y su configuración técnica. En esta guía, vamos a ver paso a paso cómo configurar y administrar un servidor web desde los cimientos hasta la seguridad avanzada.

## Paso 1: Montar el HomeLab 🔬


Para esta práctica, vamos a utilizar un entorno controlado. En mi caso, el laboratorio se basa en VirtualBox corriendo una .ova de Ubuntu 24.04.


### Realizar Snapshot 📸


Lo primero que debemos hacer antes de empezar a trabajar es realizar una instantánea o snapshot.


Un snapshot es como un punto de guardado que nos va capturar la configuración del sistema de forma exacta. De tal forma que, si algo sale mal durante la configuración, podremos restaurar el HomeLab desde el principio sin perder tiempo y recursos en reinstalarlo.


### ¿Cómo se realiza una snapshot?


**En proceso...**


## Paso 2: Instalación de herramientas básicas 🧰
Como Administradores debemos tener varias herramientas básicas para trabajar cómodamente en la terminal.
Estas herramientas básicas van a ser `nginx`, `curl`, `Net-Tools`, `htop`, `sed` y `tar`.


Antes de la instalación, al ser una máquina nueva debemos realizar un `apt update` y `apt upgrade` para asegurarnos de que todo funcione correctamente.


Como buenos Administradores de Sistemas, vamos a usar un script para instalar los programas de forma automática. Usaremos el script llamado `InstalacionBasica.sh`

``` bash
# Ejecución del script

sudo ./InstalaciónBasica.sh
```


## Paso 3: Crear la web 🌐
Para crear una web en Nginx primero necesitamos un sitio donde guardar los archivos de cada web. En linux se guardan dentro del directorio `/var/www`. Dentro de este directorio, por defecto habrá una carpeta dentro llamada `/html` que tendrá un archivo `index.html`  con un mensaje de bienvenida generado automáticamente por Nginx.
(Imagen)

Para nuestro HomeLab vamos a ignorar la carpeta `/html` y vamos a crear una propia para nuestra web. En mi caso, la carpeta se llamará web1. 
(Imagen)

Dentro de nuestra carpeta crearemos un archivo llamado `index.html` (Nota: El archivo puede ser nombrado como uno desee mientras acabe en `.html`).
Dentro de este archivo crearemos, en formato html, la página que queremos, en un entorno profesional, la información se te será proporcionada por la empresa, pero para esta práctica puedes poner algo sencillo o generar un html con IA.
