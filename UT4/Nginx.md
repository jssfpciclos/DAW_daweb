# Guía rápida a Nginx

**Recursos**

- Manuales/Turoriales
  - [Nginx Docs](https://nginx.org/en/docs/)
  - [Directivas](https://nginx.org/en/docs/dirindex.html)

- OpenWebinars: 
  - [Laboratorio de introducción a la administración de servidores web](https://openwebinars.net/academia/aprende/admin-sistemas-nginx-introduccion/)
  


## ¿Cómo entener la configuración de un servidor Nginx?

Localizar y entener la configuración de un servidor Nginx es sencillo, cómo veremos a continuación.


### 🔌 Instalar NGINX

<img src="https://github.com/jssfpciclos/DAW_eedd/assets/72703706/465e2d4b-6039-4fe6-9f7a-2c1fb3913b0d" style="display: block; margin: 0 auto;" width="400px"><br>

La forma más sencilla de instalar Nginx es usando el gestor de paquetes de tu distribución. En el caso de Ubuntu/Debian, puedes usar el siguiente comando:

```bash
sudo apt update
sudo apt install nginx
```

Para sistemas basados en Red Hat, puedes usar el siguiente comando:

```bash
sudo yum install epel-release
sudo yum install nginx
```

#### 🐋 En Docker

Si prefieres usar Docker, puedes usar el siguiente comando para descargar la imagen oficial de Nginx y ejecutar un contenedor.

```bash
docker run --name some-nginx -d -p 8080:80 nginx
```

Pero también puedes indicar alguna versión especifica, por ejemplo:

```bash
docker run --name some-nginx -d -p 8080:80 nginx:1.21.0
```

o incluso puede ser una versión alpine, que es una versión más ligera de la imagen.

```bash
docker run --name some-nginx -d -p 8080:80 nginx:1.21.0-alpine
```
o si la quieres basada en en Ubuntu

```bash
docker run --name some-nginx -d -p 8080:80 nginx:1.21.0-ubuntu
```

en debian

```bash
docker run --name some-nginx -d -p 8080:80 nginx:1.21.0-debian
```

o en centos

```bash
docker run --name some-nginx -d -p 8080:80 nginx:1.21.0-centos
```

en fin, hay muchas opciones, puedes ver todas las opciones en el [repositorio oficial de Nginx en Docker Hub](https://hub.docker.com/_/nginx).


#### ▶️ Comandos básicos

Estos son los comandos básicos para interacturar con tu instancia de Nginx.

- **Chequear versión de Nginx**<br>
  Imprime la versión
  ```bash
  nginx -v
  ```
- **Chequear configuración es correcta**<br>
  Valida la sintaxis para asegurar que no existen problemas en la configuración.  
  ```bash
  nginx -t  
  ```
- **Muestra la actualiza configuración**
  Muestra la configuración la cual es actualmente utilizada por el servidor.
  ```bash
  nginx -T
  ```
- **Recargar configuración**
  Recarga la configuración sin cerrar las conexiones activas.
  ```bash
  nginx -s reload
  ```

#### 🚀 Arrancar y parar Nginx

  Dependiendo de tu sistema, puedes usar uno de los siguientes comandos para arrancar, reiniciar, recargar la configuración o detener Nginx.

  Se puede usar el comando `systemctl` para interacturar con el servicio de Nginx

  ```bash
  sudo systemctl start nginx  # arrancar
  sudo systemctl stop nginx   # parar
  sudo systemctl restart nginx  # reiniciar
  sudo systemctl reload nginx  # recargar
  ```

  o el comando `service`

  ```bash
  sudo service nginx start  # arrancar
  sudo service nginx stop   # detener
  sudo service nginx restart # reiniciar 
  sudo service nginx reload # recargar
  ```

  dependiendo de tu sistema, puedes usar uno u otro.


### 📂 Estructura de directorios

Nginx tiene una estructura de directorios muy sencilla. La configuración por defecto se encuentra en el directorio `/etc/nginx/`. Los ficheros de configuración se encuentran en el directorio `/etc/nginx/conf.d/` y los ficheros de logs en `/var/log/nginx/`.

```bash
/etc/nginx/
├── conf.d/
│   ├── default.conf
│   └── example.com.conf
├── fastcgi_params
├── mime.types  
├── nginx.conf
├── scgi_params
└── uwsgi_params
```

La ubicación de los `assets` (imágenes, css, js, etc) depende de la distribución (debian, ubuntu, ..) por defecto es `/usr/share/nginx/html/`, aunque esta ubicación puede ser modificada en el fichero de configuración `nginx.conf`, y en los ficheros de configuración de los servidores virtuales.

#### ▶️ Localizaciones de los archivos de configuración

La configuración por defecto de Nginx se encuentra en el directorio `/etc/nginx/`.

- **Fichero principal**<br>
  `/etc/nginx/nginx.conf`

- **Directorio de configuraciones**<br>
  La mejor forma de configurar tu instancia de Nginx es poner todas las configuraciones personalizadas en el directorio `/etc/nginx/conf.d/` y luego usar la directiva `include` en el fichero `nginx.conf` para incluir estos ficheros.<br>
  Para incluir los ficheros dentro del `conf.d` usa la directiva `include /etc/nginx/conf.d/*;` en el fichero `nginx.conf`.
  
#### ▶️ Contextos de configuración

El fichero de configuración consiste de una combinación de contextos y directivas.

Cada configuración tiene:

- Un contexto principal (Main)
- Un contexto HTTP


<img src="https://github.com/jssfpciclos/DAW_eedd/assets/72703706/2eb8c291-df46-498e-b9a9-8fd75b9eb5a1" style="display: block; margin: 0 auto;" width="400px"><br>

1. **Contexto principal**<br>
Este contexto es el de más alto nivel y contiene las directivas que afectan a la configuración global del servidor.

- El número de procesos que se ejecutan
- El usuario de linux que ejecuta el servidor
- La localización del fichero Process ID (PID)

2. **Contexto Events**<br>
   Es usado para definir las directivas que afectan a la conexión del servidor, el núermo de conexiones asignadas a cada `proceso worker` y el número máximo de conexiones que el servidor puede manejar.

3. **Contexto HTTP**<br>
   Define cómo Nginx procesa las conexiones HTTP y HTTPS. Las directivas usadas sobre este contexto son heredadas por los contextos hijos, estos son el `Upstream`, `Server` y `Location`. El contexto **servidor** define los servidores virtuales (virtual hosts), los cuales procesan una petición HTTP/S para.

   - Un nombre de dominio
   - Una dirección IP
   - Un puerto (Unix socket)
  
4. **Contexto Location**<br>
   Este contexto define como los servidores virtuales procesan las peticiones basadas sobre una URI específica que tu has definido. Puede apuntar a una ruta (path) sobre el sistema de ficheros, o ser determinada por una expresión regular, o un texto definido en el contexto.

5. **Contexto Upstream**<br>
   Este contexto define un grupo de servidores que pueden ser usados para manejar las peticiones. Puede ser usado para balancear la carga entre los servidores, o para definir un servidor de respaldo en caso de que el servidor principal falle.

6. **Contexto Stream**<br>
    Este contexto es usado para definir cómo Nginx maneja la capa 3 y 4 de la red, como TCP y UDP.


#### ▶️ Directivas y bloques

Usamos las directivas para lograr una funcionalidad específica dentro de la configuración de Nginx.

- Una **directiva** es una instrucción que controla un comportamiento específico.
- Un **bloque** es un grupo de directivas agrupadas por curly braces `{}`.


<img src="https://github.com/jssfpciclos/DAW_eedd/assets/72703706/62abd70f-a810-4301-a74d-588c98df033b" style="display: block; margin: 0 auto;" width="400px"><br>


> 🧿 En profundidad <br>
> En el siguiente video se explican todos estos conceptos más en profundida realizando una demostración

#### Guía completa

[![Aprender correcta configuración lógica contextos en Nginx](https://i3.ytimg.com/vi/C5kMgshNc6g/maxresdefault.jpg)](https://youtu.be/C5kMgshNc6g)
