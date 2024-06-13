# Examen Final Extraordinaria - Despliegue de Aplicaciones Web

### Datos del alumno

- Nombre alumno:
- Curso:
- Fecha:
- Evaluación:

Este ejercicio consiste en preparar para despliegue una Aplicación Web realizada en PHP. La aplicación es una página de un hotel, que además de ser la página oficial, también tiene una parte `Administradción`, donde se realiza la gestión de las habitaciones reservadas, etc...

Esta web utiliza una base de datos MySQL, por lo que es necesario tener una base de datos MySQL para poder probar la aplicación en local.

Pero antes de poder desplegar, es necesario poder probar nuestra aplicación en local. Por ello los pasos a seguir son los siguientes:

- Crear una configuración de carpetas adecuada para el proyecto, que contenga el código fuente de la aplicación, así como los ficheros de configuración necesarios.
- Probar la aplicación en local con Docker. (A través de docker-compose)

### ENTREGA

- Se debe entregar un fichero comprimido con la estructura de carpetas y ficheros necesarios para poder probar la aplicación.
- El nombre del fichero comprimido debe ser el siguiente: `examen.eval_extra.{tu-nombre}.zip`
- Subir el fichero comprimido al Moodle.

## Partes del ejercicio

### Aplicación Web PHP

Se está desarrollando una aplicación web PHP, para un blog. Esta aplicación almacenará los datos en una base de datos MySQL.

El código fuente de la aplicación se encuentra disponible en el siguiente [enlace Hotel.zip](https://drive.google.com/file/d/1xiNij37pMGwEboD5hJ40QN7S5yTFj9Iw/view?usp=sharing)

La aplicación requiere de una BD MySQL, cuya configuración de acceso se configure en el archivo `db.php`, **se requiere cambiar esta configuración, tanto `nombre-servidor`, `usuario`, `contraseña` y `nombre-base-datos`**, según los datos de acceso a la base de datos que se configuren.

### Nginx-PHP

Para poder probar la aplicación en local, se va a utilizar una imagen de Docker que ya tiene configurado un servidor web Nginx y el servidor de aplicaciones PHP-FPM.

La confgiuración de Nginx por defecto (solo existe este servidor) es la que se indica en el siguiente fichero:

```nginx
server {
    listen       80; #ipv4
    server_name   _; # cualquier dominio

    root   /var/www/html/public;

    if ($request_method = POST) {
        set $skip_cache 1;
    }

    client_max_body_size 5M;

    location / {
        try_files $uri $uri/ $uri.php;

        # Client IP Handling for AWS ELB
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location ~ \.php$ {
        root /var/www/html/public;

        fastcgi_cache dwchiang;
        fastcgi_cache_valid 200 204 60m;
        fastcgi_ignore_headers Cache-Control;
        fastcgi_no_cache $skip_cache $http_authorization $cookie_laravel_session;
        fastcgi_cache_lock on;
        fastcgi_cache_lock_timeout 10s;
        fastcgi_buffer_size 6144;

        add_header X-Proxy-Cache $upstream_cache_status;

        fastcgi_pass            127.0.0.1:9000;
        fastcgi_index           index.php;
        fastcgi_param           SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param           HTTPS $fastcgi_param_https_variable;
        fastcgi_read_timeout    900s;
        include                 fastcgi_params;
    }

    location ~* \.(jpg|jpeg|png|gif|ico|css|js|eot|ttf|woff|woff2)$ {
        expires max;
        add_header Cache-Control public;
        add_header Access-Control-Allow-Origin *;
        access_log off;
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

### Docker

Para poder probar la aplicación en local, se va a utilizar un fichero docker-compose que levante dos contenedores, uno con la aplicación web y otro con la base de datos MySQL.

#### Docker-compose

Se dispone de un fichero `docker-compose.yml` base que hay que configurar con la configuración específica para este caso.

1. Dispone de 2 servicios, uno para la aplicación web y otro para la base de datos MySQL.

   1. Servcio `www`:

      - Se basa en la imagen `jssdocente/nginx-php-fpm:8.2`, que ya tiene configurado un servidor web Nginx y el servidor de aplicaciones PHP-FPM.
      - El servicio web esucha por el puerto 80, y se debe acceder a través de `http://localhost`.
      - El servicio web debe montar un directorio `app_hotel` que contiene el código fuente de la Web, en la ruta adecuada según se indica en la configuración de Nginx (indicada anteriormente).
      - La configuración de Nginx indicada se debe montar también para que se aplique, en la ubicación/nombre-archivo adecuada.
        (Usar para esto el fichero de configuración _default.conf_, **no hace falta crear un nuevo fichero**.)

   2. Servicio `db`:

      - Se basa en la imagen `mysql:8.0`.
      - El puerto interno de la base de datos es el 3306, pero para evitar conflictos con una posible base de datos MySQL que se esté ejecutando en el equipo, se debe utilizar de forma externa el puerto `3390`.
      - El nombre de la BD, así como el usuario y contraseña, se indican en el fichero `docker-compose.yml` como variables de entorno.
      - El nombre del servidor de BD es el nombre del servicio `db`.
        (_Para conocer el significada de cada variable de entorno, consulta la documentación de la imagen de MySQL en DockerHub_)

      - Para almacenar los datos de la base de datos, se ha creado un volumen `evfext_dbdata`. Se debe mapear el volumen a la ruta `/var/lib/mysql` del contenedor.
      - Para inicializar la base de datos, se debe montar un directorio `init` que contiene los scripts de inicialización de la base de datos, en la ruta `/docker-entrypoint-initdb.d` del contenedor.
        Los datos de inicialización deben estar ubicados en el directorio `conf/db/init/` de la estructura de carpetas del proyecto. El script de inicialización se debe llamar `init.sql`. (Este script está disponible en la carpeta raiz del comprimido con el nombre `hoteldb.sql` del código fuente de la App)

```yaml
version: "3.8"
name: exeval_extra
services:
  www:
    image: jssdocente/nginx-php-fpm:8.2
    container_name: evfext-nginx
    # ... completa la configuración del servicio www

  db:
    image: mysql:8.0
    container_name:
      evfext-mysql-8.0
      # ... completa la configuración del servicio www

    command: --default-authentication-plugin=mysql_native_password
    environment:
      MYSQL_DATABASE: hoteldb
      MYSQL_USER: hotel_user
      MYSQL_PASSWORD: 1234
    volumes:
      - ./config/db/init:/docker-entrypoint-initdb.d

volumes:
  evfext_dbdata:
    driver: local
```

> ‼️ **IMPORTANTE**: NO SE PUEDE MODIFICAR EL DOCKER-COMPOSE, SOLO AGREGAR LAS CONFIGURACIONES NECESARIAS.

### Pasos de la tarea

- [ ] 1.1 Crear la estructura de carpetas para probar la aplicación en local (0,5 puntos)
- [ ] 1.2.1a Crear el fichero docker-compose y explicación del mismo, para probar la aplicación en local. (1,5 puntos)
- [ ] 1.2.1b Conexión a la BD desde MySQL Workbench, mostrando la estructura de la BD, y los datos de las tablas `room`, `login`. (0,5 punto)
- [ ] 1.3 Aplicación Web funcionando a través de `localhost` (1,5 punto)
- [ ] 1.4 Modifica el fichero de configuración de Nginx para que se pueda acceder por el dominio `myhotel.local` y `www.myhotel.local`. (0,5 puntos)
- [ ] 1.5 Accede a la Aplicación a la parte de administración con un usuario válido según se recoge en la BD. (0,5 puntos)
      (`http://myhotel.local/admin/index.php`)
- [ ] 1.6 Crea un nuevo usuario `javier` y password `javier` en la tabla adecuada de la BD, y accede a la aplicación con este usuario. (0,5 puntos)
- [ ] 1.7 Reserva de una habitación. (0,5 puntos)
- [ ] 1.8 Lista imágenes al acceder a `myhotel.local/images` y muestra la lista de imágenes. (1 punto)
- [ ] 1.9 Página personalizada para error 403 (Forbidden) (0,3 puntos)
- [ ] 1.10 Modificación configuración Nginx solucionar problema 403 Forbidden, cuando se accede sin poner ninguna página específica. (0,5 puntos)
- [ ] 1.11. Crear imagen docker a partir de DockerFile utilizando como base la imagen `nginx:1.25.3-alpine` (0,5 puntos)
- [ ] 1.12. Crear contenedor en base al DockerFile y probar la apliación en local. (0,5 puntos)
- [] 1.13. Subir contenedor en base a DockerHub (0,5 puntos)

## Partes a entregar

### 1.1 Estructura de carpetas

Se debe crear una estructura de carpetas adecuada para el proyecto, que contenga el código fuente de la aplicación, así como los ficheros de configuración necesarios, tanto para probar probar la configuración, como para empaquetar para el despliegue.

Estructura:

```plaintext
  |-- src
      |-- app_hotel: Contiene el código fuente de la aplicación web.
      |-- config:
        |-- db:
          | -- init: Contiene los scripts de inicialización de la base de datos.
        |-- nginx: Contiene el fichero de configuración de Nginx.

      |-- Dockerfile
      |-- docker-compose.yml
  |-- examen.eval_extra.{tu-nombre}.md  : Fichero con las respuestas a las preguntas y todos los apartados del examen
```

> 📄 Explica cada una de las carpetas y archivos, indicando que funcionalidad tiene, qué ficheros se van a alojar en ella, explicando para cada uno de ellos su función/utilidad.

> 🧲 Captura de la estructura de carpetas, donde se visualize claramente el nombre de las carpetas y archivos.

### 1.2 Entrega de la configuración de docker-compose

Comenta las líneas del fichero `docker-compose.yml` que has incluiudos, indicando qué hace cada línea, a través de un comentario en el propio fichero.

> 🧲 Incluye aquí una captura de pantalla del fichero docker-compose.yml con todas las partes necesarias rellenas.

> 🧲 Incluye un GIF con la ejecución del comando `docker compose up`

> 🧲 Incluye un GIF donde se visulize la conexión desde _MySQL Workbench_ a la BD. Muestra la estructura de la BD, mostrando la estructura de la BD, y los datos de las tablas `contact`, `room` y `roombook`.

### 1.3 Entrega Aplicación Web funcionando

> 🧲 Incluye un GIF con la ejecución de la aplicación web a través de `localhost`. Accede a la misma a través del Navegador. `http://localhost/index.php`

### 1.4 Modifica configuración Nginx

Ahora realiza los cambios necesarios en la configuración de Nginx, para que esta web se pueda acceder a través del dominio `myhotel.local` y `www.myhotel.local`.<br>
Usar para esto el fichero de configuración `default.conf`, **no hace falta crear un nuevo fichero**.

> 📄 Explica qué has cambiado en la configuración de Nginx

> 🧲 Captura pantalla configuración Nginx donde se resalte el cambio realizado

### 1.5 Accede a la Aplicación con un usuario Admin

Los usuarios Administradores, están en la tabla `login` de la base de datos. Accede a la aplicación con un usuario Admin disponible en la tabla.

> 📄 Indica las credenciales de un usuario Admin

> 🧲 Adjunta GIF donde se visualize login, entrar en algunas opciones, y después Logout.

### 1.6 Crear un nuevo usuario `javier` y password `javier`

Crea un nuevo usuario `javier` y password `javier` en la tabla adecuada de la BD, y accede a la aplicación con este usuario.

> 🧲 Adjunta GIF donde se visualize login con el nuevo usuario y después Logout.

### 1.7 Reserva de una habitación

Para reservar una habitación, ir al final de la página, y click sobre `Book Now`. Esto te llevará `http://myhotel.local/reservation.php` donde podrás realizar la reserva.
Después de realizar la reserva, entra en `http://myhotel.local/admin/index.php` y comprueba que la reserva se ha realizado correctamente.

> 🧲 Adjunta una imagen donde se visualize la reserva realizada.

> 🧲 Adjunta una imagen donde se visualize que la reserva se ha realizado correctamente (`http://myhotel.local/admin/home.php`) en menu `status` deberás ver un registro de la reserva realizada.

### 1.8 Lista imágenes al acceder a `myhotel.local/images` y muestra la lista de imágenes.

Realiza la configuración necesaria en Nginx para que al acceder a `myhotel.local/images` se muestre un listado de imágenes, como si fuera una lista de ficheros.
(💡 _Recuerda reiniciar Nginx para aplicar el cambio, o reinicia el contenedor._)

> 📄 Explica qué has cambiado en la configuración y explica el motivo.

> 🧲 Incluye un GIF donde se visualize que al acceder `myhotel.local/images` se muestra la página `403.html`

### 1.9 Página personalizada para error 403 (Forbidden)

Si accedes a `localhost` o `myhotel.local` verás que obtienes una página `403 Forbidden` propia de Nginx. <br>
Crea una página personalizada para el error 403, llamada `403.html` y configura Nginx para que muestre esta página en lugar de la página por defecto.<br>

Utiliza el siguiente código HTML para la página de error 403:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>403 Forbidden</title>
  </head>

  <body>
    <h1>403 Forbidden</h1>
    <p>Lo siento, no tienes permiso para acceder a esta página.</p>
  </body>
</html>
```

### 1.10 Modifica configuración Nginx solucionar problema 403 Forbidden si no se especifica página

Si accedes a `localhost` o `myhotel.local` verás que obtienes una página `403 Forbidden`. Corrige la configuración de Nginx para que se pueda acceder a la aplicación sin especificar una página. (Hazlo a través del fichero de configuración de Nginx que se monta en el contenedor).

> 📄 Explica qué has cambiado en la configuración y explica el motivo.

> 🧲 Incluye un GIF donde se visualize que se puede acceder por `myhotel.local` y se accede a la web.

### 1.11 Crear imagen docker a partir de DockerFile

Crea un fichero `Dockerfile` que genere una imagen de Docker con la configuración aplicada al docker-compose, utilizando la imagen `nginx:1.25.3-alpine` como base.<br>
Agrega los comandos necesarios para copiar el fichero de configuración de Nginx, y el código fuente de la aplicación.
(💡 _Puedes revisar algún ejercicio anterior._)

Utiliza el nombre de la imagen `{usuario-docker-hub}/evfext-nginx` y versión 1.0.

> 🧲 Adjunta un GIF donde se visualice la creación de la imagen correctamente.

### 1.12 Subir contenedor en base a DockerHub

Sube la imagen a DockerHub creada`

> 🧲 Adjunta un imagen de tu dockerhub donde se visualize la imagen docker subida

<br>
<hr>
<br>
