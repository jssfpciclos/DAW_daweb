# UT6. Tarea Evaluable 6.1 - Desplegar aplicación PHP en Droplets de Digital Ocean

### Objetivos

- Conocer la plataforma Digital Ocean.
- Conocer los servicios que ofrece Digital Ocean.
- Crear un Droplet en Digital Ocean.
- Desplegar una aplicación PHP en un Droplet de Digital Ocean.
- Conocer y configurar los servicios de red implicados en el despliegue de una aplicación web.

### Alcance

Este ejercicio trata de 3 partes:

1. Crear y configurar un sevidor Ubuntu en Digital Ocean a través de un Droplet.
2. Configurar SSH, Firewall, Nginx y PHP en el servidor.
3. Desplegar la aplicación PHP en el servidor.

### Recursos

Para la realización de esta práctica vamos a utilizar los siguientes recursos:

- [PHP & DigitalOcean](https://youtu.be/QWSwuhQ1O6Y)
- [Configurar Dominio y SSL en Nginx](https://youtu.be/HBsCuZlDg60)


### Crear Proyecto

Antes de nada vamos a crear un proyecto en Digital Ocean, y agregar todos los recursos que vayamos creando en este tarea a este proyecto.

1. Acceder a [Digital Ocean](https://www.digitalocean.com/).
2. Crear un proyecto con el nombre `DAWeb-TE-6.1`.
3. Descríbelo como `2324 - Módulo DAWeb - Tarea Evaluable 6.1`.
4. Indica el propósito `Class project - Educational purposes`.
   

Una vez realizado esto, en DigitalOcean click sobre el nuevo proyecto creado, y comenzamos a crear. 


### Ejercicio 6.1.1 Crear Droplet en Digital Ocean

En este ejercicio vamos a crear un Droplet en Digital Ocean, dentro del proyecto creado.

Antes de nada, necesitamos tener una clave SSH.

#### Agregar clave SSH Digital Ocean

Para poder acceder a los servidores que creemos en Digital Ocean, necesitamos una clave SSH. Vamos a utilizar la misma clave SSH que hemos usado durante el curso. _Si para `casa` tienes otra clave SSH distinta, también puedes agregarla a Digital Ocean._

   1. Acceder al panel de control de Digital Ocean.
   2. En el menú de la izquierda, seleccionar `Settings` -> `Security` -> `SSH keys`.
   3. Agregar la clave SSH que tienes en tu equipo.
      - Acceder a la carpeta `~/.ssh` y copiar el contenido del fichero `*.pub`. _Sólo debes tener uno._
   4. Click en `Add SSH Key`.
   5. Añadir un nombre descriptivo para la clave SSH, por ejemplo `Instituto`, y para la de casa `Casa`.
   6. Y ya tienes tu clave SSH agregada a Digital Ocean.

#### Crear Droplet

1. Acceder a [Digital Ocean](https://www.digitalocean.com/), y al proyecto `DAWeb-TE-6.1`.
2. Crear un Droplet con las siguientes características:
   - **Elegir una imagen**: Ubuntu 22.04 (LTS) x64
   - **Elegir un plan**: Basic, $5/mo
   - **Elegir una región-datacenter**: Frankfurt
   - **Droplet Tipo**: (Shared-CPU) Basico
   - **CPU Options**: Regular (Disk-type: SSD), 6$/mo (1GB/1CPU, 25GB SSD, 1TB Transfer)
   - **Authentication**: SSH keys, Os debe indicar la clave SSH que has agregado anteriormente.
   - **Almacenamiento Adicional**: No es neceario agregar más almacenamiento.
   - **Opciones adicionales**: No es necesario añadir más opciones.
   - **Elegir a hostname**: `ubuntu-te61`
   - **Tags**: `daweb`,`te61`  (Para cada tag, pulsa TAB para que se añada)
   - **Finalizar**: Create Droplet

3. El Droplet se comenzará a crear y en unos minutos estará listo para su uso.
4. Una vez creado, tendremos una IP Pública a través de la cual podremos acceder al servidor. Vamos a necesitar esta IP para acceder al servidor.

   ```bash
   ssh root@<ip_droplet>
   ```

   y si todo está correcto, accederemos al servidor sin problemas.

> **NOTA**: Si no puedes acceder, revisa que la clave SSH que has agregado a Digital Ocean es la correcta.
  
#### Actualizar el sistema

En principio el sistema ya estará actualizado, pero por si acaso, vamos a actualizar el sistema.

```bash
sudo apt update
sudo apt upgrade
```
> 💡 **Proceso actualización**<br>
> Este proceso puede tardar unos minutos, y nos mostrará varias pantallas, sshd_config: Ha cambiado la configuración, indicar mantener y en otras pantallas, aceptar las opciones por defecto.

Por último para aplicar los cambios, reiniciamos el servidor.

```bash
sudo shutdown -r now
```

Para comprobar que el servidor se ha reiniciado correctamente, volvemos a acceder al servidor, y comprobar la versión del sistema.

```bash
lsb_release -a

No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.1 LTS
Release:        22.04
Codename:       jammy
```

### Ejercicio 6.1.2 Configurar SSH, Firewall, Nginx y PHP

#### Activar el Firewall

El firewall es una herramienta de seguridad que nos permite controlar el tráfico de red que entra y sale de nuestro servidor. Vamos a activar el firewall y permitir el tráfico de red necesario para que nuestro servidor web funcione correctamente.

> 💡 **Firewall**<br>
> UFw (Uncomplicated Firewall) es una herramienta de configuración del firewall que viene instalada por defecto en Ubuntu. Vamos a utilizar esta herramienta para configurar el firewall. [Más información](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

1. Agregar regla para permitir el tráfico de red en el puerto 80. `sudo ufw allow 80`
2. Agregar regla para permite acceso por SSH (OpenSSH) en el puerto 22. `sudo ufw allow OpenSSH`
3. Habilitar el firewall. `sudo ufw enable $$ sudo ufw status`

Una vez el firewall está configurado, vamos a comprobar que tenemos acceso a nuestro servidor de nuevo por SSH, para ello vamos a salir del servidor y volver a acceder.


#### Instalar Nginx

Para instalar Nginx, vamos a utilizar el gestor de paquetes `apt`, que previamente hemos actualizado en el apartado anterior.

```bash
sudo apt install nginx
```

Una vez instalado Nginx, también vamos a agregar una regla al firewall para permitir una regla para Nginx.

```bash
sudo ufw allow 'Nginx Full'
```

Ahora vamos a comprobar que Nginx está funcionando correctamente, para ello vamos a acceder a la IP pública de nuestro servidor a través de un navegador web, y nos tiene que mostrar la página de bienvenida de Nginx.








