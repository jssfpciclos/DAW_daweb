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

## Instalación en Ubuntu

## Pasos previos

> 💡 **Curl** (Client URL) es una herramienta de línea de comandos, que permite transferir datos hacia o desde un servidor sin interacción del usuario utilizando la biblioteca libcurl. cURL también se puede utilizar para solucionar problemas de conexión. 

Importamos la **clave GPG del repositorio** externo de Docker:

> 💡 **GPG** es un software de cifrado híbrido que usa una combinación de criptografía de claves simétricas y asimétricas para proporcionar un cifrado más fuerte que cualquiera de los dos por sí solo.

> **Repositorio externo linux** es un repositorio de software que no es parte de la distribución oficial de Debian, pero que contiene software que ha sido aprobado para su uso en Debian. Los repositorios externos se pueden usar con apt, aptitude y otros administradores de paquetes de Debian.


### Instalación usando repositorio externo (APT)

[Seguir la guía oficial](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)


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

## Primer contenedor

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