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
