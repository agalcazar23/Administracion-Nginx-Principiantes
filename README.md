# Administracion de Nginx para Principiantes 🐧

![nginx](nginx.jpeg)

A menudo, el Administrador de Sistemas recibe solicitudes para desplegar webs temporales por parte de otros departamentos. Para ello, es necesaria la creación de dominios en Nginx, la gestión de permisos y su configuración técnica. En esta guía, vamos a ver paso a paso cómo configurar y administrar un servidor web desde los cimientos hasta la seguridad avanzada.

Un Administrador de Sistemas profesional es capaz de automatizar todo esto para reducir tiempo. Recuerda que si puedes hacer algo 2 veces, lo puedes automatizar.

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

* **nginx** → servidor web
* **curl** → probar peticiones HTTP
* **htop** → monitor de procesos
* **net-tools** → herramientas de red
* **sed** → edición de texto
* **tar** → compresión

Antes de la instalación, al ser una máquina nueva debemos realizar un `apt update` y `apt upgrade` para asegurarnos de que todo funcione correctamente.


Como buenos Administradores de Sistemas, vamos a usar un script para instalar los programas de forma automática. Usaremos el script llamado `InstalacionBasica.sh`

``` bash
# Ejecución del script

sudo ./InstalaciónBasica.sh
```


## Paso 3: Crear la web 🌐
### La ruta `/var/www`


Para crear una web en Nginx primero necesitamos un sitio donde guardar los archivos de cada web. En linux se guardan dentro del directorio `/var/www`. Dentro de este directorio, por defecto habrá una carpeta llamada `/html` que contendrá un archivo `index.html`  con un mensaje de bienvenida generado automáticamente por Nginx.
(Imagen)

### Olvidar `/var/www/html`
Para nuestro HomeLab vamos a ignorar la carpeta `/html` y vamos a crear una propia para nuestra web. En mi caso, la carpeta se llamará web1. 
(Imagen)

``` bash
# Creamos nuestra carpeta

sudo mkdir /var/www/web1
```


### Crear archivo web
Dentro de nuestra carpeta crearemos un archivo llamado `index.html`.
> **NOTA**: El archivo puede ser nombrado como uno desee mientras acabe en `.html`. Esto se debe a que Nginx, por configuración predeterminada, busca un archivo que se llame exactamente `index.html`.

Dentro de este archivo crearemos, en formato `.html`, la página que queremos. En un entorno profesional, los desarrolladores son los que escriben el código y lo suben a un repositorio, pero para esta práctica puedes poner algo sencillo o generar un html con IA.


### Configurar Nginx y activar la web
Nginx guarda sus configuraciones en `/etc/nginx/sites-available/`. Crea un archivo nuevo para la web. En mi caso:

``` bash
sudo nano /etc/nginx/sites-available/web1
```

Una vez estamos dentro con el nano, pega esto:

``` bash
# Archivo de configuración de nuestra web

server {
    listen 80; # Puerto normal de internet (http)
    server_name web1.com; # EL NOMBRE DE LA WEB
    root /var/www/web1;   # LA CARPETA DONDE ESTÁ LA WEB
    index index.html;
}
```
[!TIP]> **NOTA**: Para esta práctica vamos a activar el puerto 80 que es el de http, es decir sitio no seguro, ya que el puerto 443 que es el de https nos va a poner un aviso molesto de advertencia cada vez que queramos entrar además de un mensaje de "sitio no seguro". Esto se soluciona activando una licencia que no vamos a activar para un HomeLab.


Para activar el sitio vamos a activar un acceso directo en la carpeta `sites-enabled`. Tras ello, reiniciamos el servicio para que lea los cambios. El comando de enlace simbólico `ln -s` es el método estándar y profesional de hacerlo.

``` bash
sudo ln -s /etc/nginx/sites-available/web1 /etc/nginx/sites-enabled/

sudo systemctl reload nginx
```
> **¿Por qué `reload` y no `restart`**: Restart apaga y enciende el servicio mientras que reload solo recarga la configuración sin desconectar a los usuarios que estén viendo la web. Esto último es mejor si queremos editar algo mientras la web está funcionando.

### El archivo `/etc/hosts`
Como web1.com no existe de verdad en internet, tu navegador no sabrá dónde ir. Para ello vamos a indicarle en el archivo `/etc/hosts` nuestra IP junto al nombre de la web. De esta manera podremos hacer que la página funcionará en esta máquina.

``` bash
# Escribe al final esta línea con tu IP y el nombre

192.168.1.XX web1.com
```

¡Enhorabuena! Una vez terminado este proceso, abre un navegador y escribe `http://web1.com` (o el nombre que le hayas dado a la web) y se abrirá tu web con el diseño que hayas puesto.


### <mark>LO MAS IMPORTANTE ❗</mark>
Como ya quizá habrás pensado. Este proceso es fácilmente automatizable, por lo que, como buenos administradores, vamos a usar un script para automatizar todo este proceso. El script está explicado en otro repositorio mío: [Script automatización web](https://github.com/agalcazar23/Script-Dominios-Nginx)

## Paso 4: Hardening 🛡️
