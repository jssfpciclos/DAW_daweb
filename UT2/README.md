# UT2: Introducción a Docker

![Docker](files/docker.png)

# 🗓 Recursos

<details>
  <summary><b>Terminología</b></summary>
  
  - *Images* - Son las plantillas a través de las cuales se crean los contenedores.
  - *Containers* - Creados desde las imágenes y son los que contienen la aplicación o utilidad.  Creamos un container a través de  Created from `docker run` y con `docker ps` podemos ver la lista de containers en ejecución.
  - *Docker Daemon* - el servicio en segundo plano que se ejecuta en el host que administra la creación, ejecución y distribución de contenedores Docker. El demonio es el proceso que se ejecuta en el sistema operativo con el que hablan los clientes.
  - *Docker Client* - a herramienta de línea de comandos que permite al usuario interactuar con el daemon. En términos más generales, también puede haber otras formas de clientes, como que proporciona una GUI a los usuarios..
  - *Docker Hub* - Un [registry](https://hub.docker.com/explore/) of imágenes docker.  Puede pensar en el registro como un directorio de todas las imágenes de Docker disponibles. Si es necesario, uno puede alojar sus propios registros de Docker y puede usarlos para extraer imágenes.   

 </details>

<details>
  <summary><b>Páginas de Ayuda</b></summary>

  - **Páginas de ayuda**
    - [Página oficial](https://www.docker.com/)
    - [Docker Hub](https://hub.docker.com/)
    - [Pagina referencia comandos](https://docs.docker.com/engine/reference/run/)

</details>

<details>
  <summary><b>Instalación</b></summary>

  - **Instalación**
    - [Instalación en Windows](https://docs.docker.com/docker-for-windows/install/)
    - [Instalación en Mac](https://docs.docker.com/docker-for-mac/install/)
    - [Instalación en Linux](https://docs.docker.com/engine/install/ubuntu/)

</details>
<br>


# 🏆 Objetivos

- Conocer las ventajas que nos proporciona el uso de la tecnología de contenedores.
- Conocer los conceptos principales sobre el despliegue de aplicaciones web utilizando contenedores.
- Conocer los conceptos fundamentales sobre Docker.
- Trabajar con imágenes Docker.
- Desplegar aplicaciones web sencillas en contenedores.
- Introducción al uso del almacenamiento en Docker.
- Introducción al uso de la redes en Docker.
- Ser capaz de usar contenedores de terceros y de construir mis propios contenedores.
- Creación de imágenes Docker.
- Desplegar escenarios multicontenedor usando Docker-compose.
- Estudiar el ciclo de vida del desarrollo, pruebas y despliegue de aplicaciones utilizando contenedores.
<br><br>

## ¿ Por qué Docker ?

**Video: [Docker - La explicación que querias](https://youtu.be/9eTVZwMZJsA)**

[![La explicación que querias](https://i3.ytimg.com/vi/9eTVZwMZJsA/maxresdefault.jpg)](https://youtu.be/9eTVZwMZJsAl-Y "Docker - La explicación que querias")


# 📚 Instalación

La instalación se puede realizar en cualquier sistema operativo.<br>
Como este tipo de tecnología avanza muy rápido, lo mejor es seguir la guía oficial de instalación:

- [Instalación en Windows](https://docs.docker.com/docker-for-windows/install/)
- [Instalación en Mac](https://docs.docker.com/docker-for-mac/install/)
- [Instalación en Linux](https://docs.docker.com/engine/install/ubuntu/)


## Instalación en Ubuntu

## Pasos previos

> 💡 **Curl** (Client URL) es una herramienta de línea de comandos, que permite transferir datos hacia o desde un servidor sin interacción del usuario utilizando la biblioteca libcurl. cURL también se puede utilizar para solucionar problemas de conexión. 

Importamos la **clave GPG del repositorio** externo de Docker:

> 💡 **GPG** es un software de cifrado híbrido que usa una combinación de criptografía de claves simétricas y asimétricas para proporcionar un cifrado más fuerte que cualquiera de los dos por sí solo.

> **Repositorio externo linux** es un repositorio de software que no es parte de la distribución oficial de Debian, pero que contiene software que ha sido aprobado para su uso en Debian. Los repositorios externos se pueden usar con apt, aptitude y otros administradores de paquetes de Debian.


La instalación de Docker en Ubuntu se puede realizar de varias formas:

- [Docker Desktop para Linux (Paquete con todo incluido)](https://docs.docker.com/desktop/install/linux-install/)
- Instalación usando repositorio externo (APT)
- Inslacación manual.
- Instalación usando script de instalación
  
En este caso vamos a realizar la instalación usando el repositorio externo (APT).

### Instalación usando repositorio externo (APT)

[Seguir la guía oficial](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

> 💡 **Actualizar** Para actualizar Docker Engine, repetir el proceso de instalación apuntando a la nueva versión.


## Comprobación

Lo primero de todo es comprobar que el servicio esté corriendo correctamente:

```console
sdelquin@lemon:~$ sudo systemctl status docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-09-16 12:45:28 WEST; 2min 25s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 86331 (dockerd)
      Tasks: 8
     Memory: 35.0M
        CPU: 117ms
     CGroup: /system.slice/docker.service
             └─86331 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.032847201+01:00" level=info msg="scheme \"un>
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.032854909+01:00" level=info msg="ccResolverW>
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.032893575+01:00" level=info msg="ClientConn >
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.073261246+01:00" level=info msg="Loading con>
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.154568955+01:00" level=info msg="Default bri>
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.199050947+01:00" level=info msg="Loading con>
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.226591830+01:00" level=info msg="Docker daem>
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.226646621+01:00" level=info msg="Daemon has >
sep 16 12:45:28 lemon systemd[1]: Started Docker Application Container Engine.
sep 16 12:45:28 lemon dockerd[86331]: time="2022-09-16T12:45:28.235165174+01:00" level=info msg="API listen >
```

Igualmente podemos comprobar la versión instalada:

```console
jssdocente@vm:~$ docker --version
Docker version 20.10.18, build b40c2f6
```

## Pasos posteriores

Un usuario "ordinario" no podría trabajar con Docker ya que el servicio sólo está a disposición de usuarios "privilegiados" (`root`, `sudo`). En este sentido debemos incluir a nuestro usuario habitual en el grupo adecuado:

```console
jssdocente@vm:~$ sudo usermod -aG docker $USER
```

> Para que los cambios surtan efecto, salimos de la sesión y volvemos a entrar con nuestro usuario habitual.

## El 'Hello World' de Docker

Docker nos ofrece un contenedor "[Hello World](https://github.com/docker-library/hello-world/blob/master/hello.c)" para comprobar que todo se ha instalado correctamente y que los permisos son los adecuados:

```console
jssdocente@vm:~$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
7050e35b49f5: Pull complete
Digest: sha256:62af9efd515a25f84961b70f973a798d2eca956b1b2b026d0a4a63a3b0b6a3f2
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

> 🌍 **Repositorio Docker** es un servicio que permite a los usuarios de Docker distribuir imágenes de Docker de forma privada o pública. Un registro es un servicio centralizado para almacenar y distribuir imágenes.

Pero, ¿qué es lo que está sucediendo al ejecutar esa orden?:

- Al ser la primera vez que ejecuto un contenedor basado en esa imagen, la imagen `hello-word` se descarga desde el repositorio que se encuentra en el registro que vayamos a utilizar, en nuestro caso DockerHub.
- Muestra el mensaje de bienvenida que es la consecuencia de ejecutar un comando al crear y arrancar un contenedor basado en esa imagen.

Si listamos los contenedores que se están ejecutando (`docker ps`):

```
**$ docker ps**
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

Comprobamos que este contenedor no se está ejecutando. **Un contenedor ejecuta un proceso y cuando termina la ejecución, el contenedor se para.**

Para ver los contenedores que no se están ejecutando:

```
**$ docker ps -a**
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
372ca4634d53        hello-world         "/hello"            8 minutes ago       Exited (0) 8 minutes ago                       elastic_johnson
```

Para eliminar el contenedor podemos identificarlo con su `id`:

`$ docker rm 372ca4634d53`

o con su nombre:

`$ docker rm elastic_johnson`
 

 ## Conceptos básicos

 ### Imágenes

Una imagen es un paquete ejecutable que incluye todo lo necesario para ejecutar una aplicación (código, librerías, variables de entorno, herramientas del sistema, etc.). Las imágenes se definen mediante un fichero de texto llamado *Dockerfile*.

Las imágenes se pueden crear a partir de otras imágenes, añadiendo o quitando componentes, o bien se pueden descargar de un repositorio de imágenes. **Las imágenes se almacenan en un registro de imágenes**.

### Contenedores

Un contenedor es una instancia en ejecución de una imagen. **Un contenedor ejecuta un proceso y cuando termina la ejecución, el contenedor se para.**

### Registros

Un registro es un servicio centralizado para almacenar y distribuir imágenes. **Un registro puede ser público o privado**. Docker Hub es un registro público que cualquiera puede usar, y Docker es el registro por defecto para Docker.

### Dockerfile

Un `Dockerfile` es un fichero de texto que contiene las instrucciones necesarias para crear una `imagen`.

### Docker Compose

Docker Compose es una herramienta que permite definir y ejecutar aplicaciones Docker multicontenedor. Con Compose, se utiliza un fichero YAML para configurar los servicios de la aplicación. Luego, con un solo comando, se crea y arranca todos los servicios desde la configuración.

## Comandos básicos

### Imágenes

- Para listar las imágenes que tenemos en nuestro sistema:<br>
   `$ docker images`

- Para descargar una imagen desde un registro:<br>
   `$ docker pull <nombre_imagen>`

   > ▶️ Ejemplo: `$ docker pull ubuntu`


- Para eliminar una imagen:<br>
   `$ docker rmi <nombre_imagen>`
   > ▶️ Ejemplo: `$ docker rmi ubuntu`

### Contenedores

- Para listar los contenedores que tenemos en nuestro sistema:<br>
   `$ docker ps`

- Para listar todos los contenedores que tenemos en nuestro sistema:<br>
   `$ docker ps -a`

- Para crear un contenedor a partir de una imagen:<br>
   `$ docker run <nombre_imagen>`
   > ▶️ Ejemplo: `$ docker run ubuntu`

- Para crear un contenedor a partir de una imagen con un nombre específico:<br>
   `$ docker run --name <nombre_contenedor> <nombre_imagen>`
   > ▶️ Ejemplo: `$ docker run --name ubuntu1 ubuntu`
   
- Para crear un contenedor a partir de una imagen y que sea interactivo:<br>
   `$ docker run -it <nombre_imagen>`
   > ▶️ Ejemplo: `$ docker run -it ubuntu`

- Para crear un contenedor a partir de una imagen y que sea interactivo y que el puerto 80 del contenedor se mapee al puerto 8080 del host:<br>
   `$ docker run -it -p 8080:80 <nombre_imagen>`
   > ▶️ Ejemplo: `$ docker run -it -p 8080:80 ubuntu`

- Para crear un contenedor a partir de una imagen y que sea interactivo y que el directorio `/var/www/html` del contenedor se mapee al directorio `/home/jssdocente/html` del host:<br>
   `$ docker run -it -v /home/jssdocente/html:/var/www/html <nombre_imagen>`
   > ▶️ Ejemplo: `$ docker run -it -v /home/jssdocente/html:/var/www/html ubuntu`


## 🧹 Limpiando recursos

Hay un paquete muy interesante de cara a la "limpieza" de recursos Docker. Se llama [docker-clean](https://github.com/ZZROTDesign/docker-clean) y se puede instalar de la siguiente manera:

`$ sudo apt install -y docker-clean`

Uno de los comandos más cómodos de este paquete es: `docker-clean run` que se encarga de borrar:

- Todos los contenedores parados.
- Todas las imágenes sin etiquetar.
- Todos los volúmenes sin usar.
- Todas las redes virtuales.

<br><br>

# Trabajo con Docker

<details>
  <summary><b>Ejecución simple de contenedores</b></summary>

   Con el comando `run`  vamos a crear un contenedor donde vamos a ejecutar un comando, en este caso vamos a crear el contenedor a partir de una imagen ubuntu. Como todavía no hemos descargado ninguna imagen del registro docker hub, es necesario que se descargue la imagen. Si la tenemos ya en nuestro ordenador no será necesario la descarga.

```bash
**$ docker run ubuntu echo 'Hello world'**

Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
8387d9ff0016: Pull complete
...
Status: Downloaded newer image for ubuntu:latest
Hello world
```

Comprobamos que el contenedor ha ejecutado el comando que hemos indicado y se ha parado:

```bash
$ docker ps -a

CONTAINER ID        IMAGE              COMMAND                  CREATED s              STATUS                      PORTS               NAMES
3bbf39d0ec26        ubuntu              "echo 'Hello wo…"   31 seconds ago      Exited     (0) 29 seconds ago                       wizardly_edison
```

Con el comando `docker images`
 podemos visualizar las imágenes que ya tenemos descargadas en nuestro ordenador.

</details>

<br>

<details>
  <summary><b>Ejecutando Ubuntu como un Docker Container</b></summary>

Más que instalar Ubuntu en una máquina virtual, podemos ejecutar Ubuntu como un contenedor de Docker. Esto es posible porque Docker proporciona una imagen de Ubuntu en su repositorio de imágenes. Para ejecutar Ubuntu como un contenedor de Docker, primero debemos descargar la imagen de Ubuntu del repositorio de imágenes de Docker usando el comando `pull` :

### Paso 1: Obtener la imagen de Ubuntu

```bash
**$ docker pull ubuntu**
```

> 💡 Esto no es necesario, con la orden `docker run` se descarga la imagen si no la tenemos en nuestro ordenador.

Si estamos interesados en una versión específica de Ubuntu, podemos indicar la versión específica en el nombre de la imagen. Por ejemplo, para descargar la imagen de Ubuntu 18.04, podemos usar el siguiente comando:

```bash
**$ docker pull ubuntu:18.04**
```

### Paso 2: Ejecutar la imagen de Ubuntu

```bash
sudo docker run -ti --rm ubuntu:22.04 /bin/bash
```

- El comando anterior ejecutará la imagen de Ubuntu 22.04 como un contenedor de Docker. 
- El parámetro `-ti` se utiliza para iniciar el contenedor en modo interactivo. - El parámetro `--rm` se utiliza para eliminar el contenedor cuando se detiene. 
- El parámetro `/bin/bash` se utiliza para ejecutar el shell Bash dentro del contenedor.

> ▶️ La imagen de Docker no tiene ningún GUI instalado, por lo que no podremos ejecutar ninguna aplicación GUI dentro del contenedor.

El shell inicia como un usuario `root` y la temrinal es similar a lo que esperas de un sistema Ubuntu normal.<br>
Por defecto, el contenedor tiene un nombre de host aleatorio. Para cambiar el nombre de host, puede usar el parámetro `--hostname` :

```bash
**$ docker run -ti --rm --hostname dckubuntu ubuntu:22.04 /bin/bash**
```

### Paso 3: Ejecutar comandos dentro del contenedor

Una vez que el contenedor se inicia en modo interactivo, puede ejecutar cualquier comando dentro del contenedor. Por ejemplo, para ejecutar el comando `ls` dentro del contenedor, puede usar el siguiente comando:

```bash
**$ ls**
bin   dev  home  lib32  libx32      media  opt   root  sbin  srv  tmp  var
boot  etc  lib   lib64  lost+found  mnt    proc  run   snap  sys  usr
```

Para revisar la versión de Ubuntu, puede usar el siguiente comando:

```bash
**$ cat /etc/os-release**
NAME="Ubuntu"
VERSION="22.04 LTS (Jammy Jellyfish)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 22.04 LTS"
VERSION_ID="22.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=jammy
UBUNTU_CODENAME=jammy
```

Y podemos instalar las aplicaciones que necesitemos usando los comandos habituales de Ubuntu:

```bash
**$ apt update**
**$ apt install tree**
```

### Paso 4: Salir del contenedor

Para salir del contenedor, simplemente escriba `exit` en la terminal.

```bash
**$ exit**
```

### Paso 5: Vida efímera del contenedor

Los contenedores de Docker son efímeros, lo que significa que se eliminan cuando se detienen. Para verificar esto, puede ejecutar el siguiente comando:

```bash
**$ docker ps -a**
```
> La opción `-a` muestra todos los contenedores, incluidos los que se han detenido.


### Volver a ejecutar el contenedor

Si desea volver a ejecutar el contenedor, puede usar el siguiente comando:

```bash
**$ docker start -ai <container_id>**
```

> La opción `-a` se utiliza para adjuntar la terminal del contenedor a la terminal del host. La opción `-i` se utiliza para iniciar el contenedor en modo interactivo.

Pero un contenedor se detiene inmediatamente después de que se complete el comando.<br>
Los contenedores son tan ligeros que son de usar y tirar, por lo que si necesitamos un contenedor con una configuración específica, lo mejor es crear una imagen personalizada.
*Esto lo veremos más adelante.*


</details>

<br>

<details>
  <summary><b>Caso práctico. Ejecutar SSH en contenedor</b></summary>
   
   ### Utilizar una imagen existente

   Para este caso práctico vamos a utilizar una imagen que ya existe en el registro de Docker Hub. Se trata de la imagen `rastasheep/ubuntu-sshd`. Esta imagen nos permite ejecutar un servidor SSH en un contenedor de Docker.

   [Página de la imagen docker](https://hub.docker.com/r/rastasheep/ubuntu-sshd)

   ### Ejemplo de uso

   1. Ejecutamos el comando

      ```bash
      **$ docker run -d -P --name test_sshd rastasheep/ubuntu-sshd:latest**
      ```

      > 💡 El parámetro `-d` se utiliza para ejecutar el contenedor en segundo plano. El parámetro `-P` se utiliza para mapear el puerto SSH del contenedor al puerto aleatorio del host. El parámetro `--name` se utiliza para asignar un nombre al contenedor.
      
      <br>
   
   2. Podemos comprobar que el contenedor se está ejecutando:

      ```bash
      **$ docker ps**
      ```

      Ahora para conectar con el contenedor, necesitamos saber el puerto SSH del contenedor. Para ello, puede usar el siguiente comando:

      **Docker port** lista los puertos o rangos de puertos que se asignan a un contenedor.

      ```bash
      **$ docker port test_sshd 22**

      22/tcp -> 0.0.0.0:32768
      22/tcp -> [::]:32768
      ```

      > 💡 Indica que el puerto 22 del contenedor se ha mapeado al puerto 32768 del host. Ahora podemos conectarnos al contenedor usando el siguiente comando:


   3. Conectar al contenedor por SSH
   
      > No necesitamos la ip del contenedor, ya que un puerto del host se mapeado (vincula) a un puerto del contenedor.

      ```bash
      **$ ssh root@localhost -p 32768**
      ```

      El usuario es `root` y la contraseña es `root`.

      Para cambiar la contraseña (ejeuctar el comando dentro del contenedor)):

      ```bash
      **$ docker exec -ti test_sshd passwd
      ```

   4. Para copiar la clave pública de nuestro usuario al contenedor:

      ```bash
      **$ ssh-copy-id root@localhost -p 32768**
      ```

      > 💡 El comando ssh-copy-id copia la clave pública de nuestro usuario al contenedor.<br>
        Si se desea indicar una clave pública específica, se puede usar la opción `-i`.<br>
        **$ ssh-copy-id -i ~/.ssh/id_rsa.pub root@localhost -p 32768**
        

      Esto se puede comprobar si revisamos el fichero `authorized_keys` del contenedor:

      > **Docker exec** ejecuta un comando en un contenedor que se está ejecutando.
      ```bash
      **$ docker exec -ti test_sshd cat /root/.ssh/authorized_keys**
      ```

   5. Conectar sin solicitar password

      Ahora podemos conectarnos al contenedor sin solicitar la contraseña:

      ```bash
      **$ ssh root@localhost -p 32768**
      ```

   6. Detener el contenedor

      ```bash
      **$ docker stop test_sshd**
      ```

   7. Eliminar el contenedor

      ```bash
      **$ docker rm test_sshd**
      ```
   

</details>


<br>

