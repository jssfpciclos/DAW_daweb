# UT2-TE2.1: Tarea Evaluable 2.1. Dockerización de stack LAMP

En esta tarea vamos a dockerizar el stack LAMP que hemos creado en el caso práctico que se indica en recursos.

### Objetivos

- Conocer las ventajas que nos proporciona el uso de la tecnología de contenedores.
- Conocer los conceptos principales sobre el despliegue de aplicaciones web utilizando contenedores.
- Conocer los conceptos fundamentales sobre Docker.
- Trabajar con imágenes Docker.
- Trabajar con Docker y docker compose (orquestación de contenedores).
- Desplegar aplicaciones web sencillas en contenedores.

### 🗓 Recursos

- [Temario del Tema UT2](../README.md)
- [Caso práctico: Dockerización de stack LAMP](../doc/caso-practico/03.lamp-docker.md)

**GIF Videos**

- [Software crear GIFs animados para Windows](https://www.screentogif.com/)
- [Software crear GIFs animados para Linux](https://github.com/phw/peek)
- [Herramienta Online GIF](https://ezgif.com/video-to-gif)

### Entregable

Informe explicando los pasos seguidos para resolver la tarea, y adjuntando las imágenes/gif que se solicitan en cada uno de los pasos.
El informe se entregará en un fichero `README.md` en el repositorio oficial del alumno, en la carpeta `UT2/TE2.1/`.<br>

Se entregará con el siguiente formato:

1. Titulo de la tarea, donde se indique el nombre de la tarea y el nombre de la asignatura, y el nombre del alumno, asi como el enlace (formato commit) al fichero (README.md) de vuestro repositorio.
2. Explicación de cada uno de los puntos, según se indica en cada uno de los pasos.

Estructura carpeta entrega (vuestro repositorio oficial):

```bash
UT2/TE2.1/README.md  (documentación principal)
UT2/TE2.1/img        (imagenes/gifs a incluir en la documentación)
UT2/TE2.1/src
  |
  +-- docker-lamp/    (código fuente de la tarea)
    |
    +-- .gitignore  (excluir ficheros no necesarios (datos de BD, etc))
    +-- docker compose.yml
```

## 📚 TAREA EVALUABLE 2.1

### Pasos iniciales

1. Descargar los [recursos de la tarea](res/Tarea2.1.recursos.rar) y descomprimir en una carpeta que llamaremos `docker-lamp`.
2. Crear una imagen de Docker que incluya Apache y PHP, a partir de la imagen oficial de PHP 8.0.0 con Apache, e incluyendo el driver de MySQL para PHP.
   1. Crear el fichero DockerFile para la creación de la imagen (Los detalles están incluidos en el [caso práctico](../doc/caso-practico/03.lamp-docker.md)).<br>
   2. Construir el DockerFile dando a la imagen `php-apache8.0-SDF` con el tag `1.0`. `docker build -t php-apache8.0-sdf:1.0 . `. (mostrar imagen que no muestra error en la creación)
   3. Mostrar que la imagen creada está disponible en el repositorio local de imágenes. `docker images`.
   4. Borrar la imagen creada.  
      <br>
      _Explicación del paso:_ - Explicar que es un DockerFile y cual es su finalidad. - Explicar que hace el código del DockerFile que habéis utilizado.

### Definir el fichero docker compose

En esta serie de pasos se debe ir creando el fichero `docker compose.yml` que permitirá crear los contenedores necesarios para el stack LAMP, se construirá por partes, y revisando si funciona cada parte

3. Definir el servicio `wwww`, que utiliza la imagen que debe construir a través del DockerFile creado en el paso anterior con los siguientes datos.<br>

   - nombre-image-crear: `daw/lamp-apache-php8-sdf:1.0`
   - nombre-contenedor: `lamp-apache-php8-sdf`
   - mapear el puerto `9000` del host al puerto `80` del contenedor.
   - mapear la carpeta `./www` del host al volumen `/var/www/html` del contenedor.

   Pasos:

   - Levantar el docker compose para verificar log en modo `atacched` y comprobar que todo funciona bien. `docker compose up --build` (_--build para reconstruir la imagen aunque ya exista_) (incluir imagen/gif) <br>
   - Comprobar desde otra terminal, que se ha construido la imagen indicada.
   - Detener/cerrar la ejecución del docker compose (Ctrl+C).
   - Limpiar los contenedores creados y eliminar la imagen creada. `docker compose down --rmi all` _--rmi elimina todas las imágenes creadas_ (incluir imagen)
     <br>
     _Explicación del paso:_ - Explicar las partes del servicio en el docker compose definido y que hace cada apartado. - ¿Qué es el modo `attached` y `detached` cuando ejecuto un contenedor o el docker compose? - Explicar que hace cada punto que se ha indicado en la configuración del servicio (build, ports, volumes, etc).

4. Definir dentro de fichero docker compose una red `network`, de nombre `lamp-network`, de tipo `bridge`, y enlazar el servicio `www` definido en el punto anterior, a esta red.
5. Definir dentro del fichero docker compose un servicio `db` para construir un contenedor para Mysql, con los siguientes datos:

   - nombre-servicio: `db`
   - contenedor: `lamp-mysql-sdf`
   - nombre-imagen: `mysql:8.0`
   - mapear el puerto `3399` del host al puerto `3306` del contenedor.
   - mapear los siguientes volumenes/carpetas:
     - `./conf` del host a la ruta `/etc/mysql/conf.d` del contenedor. (configuración de mysql)
     - `./dump` del host a la ruta `/docker-entrypoint-initdb.d` del contenedor. (scripts de inicialización de datos)
   - adjuntar a la red `lamp-network` definida en el punto anterior.
   - definir las variables de entorno `MYSQL_ROOT_PASSWORD` con valor `test` y `MYSQL_DATABASE` con valor `dbname`, y `MYSQL_USER` y `MYSQL_PASSWORD` con los valores `lamp` y `lamp` respectivamente.
   - enlazar el servicio `mysql` a la red `lamp-network` definida en el punto anterior.

   Pasos:

   - Levantar el docker compose para verificar log en modo `atacched` y comprobar que todo funciona bien. `docker compose up` (incluir imagen/gif) <br>
   - Comprobar desde el programa `MySQL Workbench` el acceso a la BD creada `dbname` (acceder con los datos de acceso configurados) [incluir gif]
   - Detener/cerrar la ejecución del docker compose (Ctrl+C).
   - Limpiar los contenedores creados y eliminar volumenes y redes. `docker compose down -v` (incluir imagen)
     <br>
     _Explicación del paso:_ - Explicar las partes del servicio en el docker compose definido y que hace cada apartado. - Explicar para qué se usan las variables en los contenedores en general y en este caso en particular. - Explicar que es una red de tipo `bridge` y que es una red `lamp-network`.

6. Definir dentro del fichero docker compose un servicio para levantar el contenedor `phpmyadmin`, con los siguientes datos:

   - nombre-imagen: `phpmyadmin/phpmyadmin`
   - contenedor: `lamp-phpmyadmin-sdf`
   - mapear el puerto `8900` del host al puerto `80` del contenedor.
   - definir las variables de entorno, `MYSQL_ROOT_PASSWORD` con valor `test` y `MYSQL_USER` y `MYSQL_PASSWORD` con los valores `lamp` y `lamp` respectivamente.
   - enlazar el servicio `phpmyadmin` a la red `lamp-network` definida en el punto anterior.

   Pasos:

   > Solo definir el servicio en el docker compose, no levantar el docker compose
   > <br>

7. Definir la precedencia de arranque de los contenedores, de tal forma que los servicios `www` y `phpmyadmin` deben esperar a que el servicio `mysql` esté en ejecución.

   Pasos:

   - Levantar el docker compose para verificar log en modo `atacched` y comprobar que todo funciona bien. `docker compose up` (incluir imagen/gif) <br>
   - Comprobar desde el navegador el acceso a phpMyAdmin (acceder con los datos de acceso configurados) [incluir gif]
   - Comprobar desde phpMyAdmin el acceso a la BD creada `dbname` (acceder con los datos de acceso configurados) [incluir gif]
   - Comprobar el acceso a la BD a través de MySQL Workbench (acceder con los datos de acceso configurados) [incluir gif]
   - Detener/cerrar la ejecución del docker compose (Ctrl+C).
   - Limpiar los contenedores creados y eliminar volumenes y redes. `docker compose down -v` (incluir imagen)

8. Probar el acceso a la aplicación web desde el navegador. (http://localhost:9000) [incluir gif]

   - Navegar a la dirección `localhost:9000` desde el navegador, y comprobar que se muestra correctamente la lista de nombres [incluir gif]

<img src="../files/lamp-working.gif " width="600px" />
