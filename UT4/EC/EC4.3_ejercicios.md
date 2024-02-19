# Ejercicios 4.3: Configuraciones avanzadas de Nginx

Recursos para el ejercicio:

- [Archivos web Mypetshop](./res/mypetshop.website.zip)
- [Listado de directivas de Nginx](https://nginx.org/en/docs/dirindex.html)
- [Referencias del UT4](../../UT4/README.md#referencias)

Para la realización de estos ejercicios, crea un nuevo directorio en tu repositorio llamado `UT4\EC\4.3`

> 🔌 **Realiza los ejercicios con Docker**<br>
> - Para la realización de este ejercicio, usa la última versión de Nginx disponible en Docker Hub.
> - Estos ejercicios se realizarán dentro del contenedor de Docker

Este ejercicio trata de 3 partes:

1. Desplegar una página web en un servidor Nginx con Docker-compose
2. Crear una imagen de docker, que contenga la configuración.
3. Desplegar el servidor Nginx con la imagen creada.


### Ejercicio 4.3.1 Despliegue con Docker-compose

Basado en el ejercicio 4.2, vamos a desplegar una página web estática, con un dominio asociado `mypetshop.local` en un servidor Nginx con Docker-compose.

> 🏷️ 
Los ficheros de la página están disponible en el siguiente enlace [Mypetshop](./res/mypetshop.website.zip).

Para esto crea la siguiente estructura de directorios:

```plaintext
UT4\EC\4.3
│   docker-compose.yml
└───config
    │   nginx
    │   └───conf.d
    │       │   mypetshop.conf
    └───app
        │   (ficheros de la página web, descomprimir el archivo mypetshop.website.zip en esta carpeta)
```

> 💡 **Objetivo**
> El objetivo es crear un servidor-virtual para alojar el sitio web de la tienda de mascotas `mypetshop.local`.

Configura el archivo `mypetshop.conf` para crear con la siguiente configuración:

- Escucha en el puerto 80
- Nombre del servidor `mypetshop.local` y `www.mypetshop.local`
- Ruta del documento raíz `/var/www/html/mypetshop.local`
- Si no se indica ningún fichero, por defecto usará `index.html`, `index.htm`, en ese orden.
- Además:
  - Servir ficheros desde la url base `\` con las siguientes indicaciones:
    - 1º, si el fichero existe, servirlo.
    - 2º, si no existe, servir la carpeta del la url base. _Ejemplo: si se accede a `http://mypetshop.local/images` y no existe un fichero `images`, intente server la carpeta `images`._
    - 3º, si no existe, devolver una página 404.
  - Permitir que la carpeta `images` sea listada, mostrando los ficheros que contiene.
  - Añade una directiva `error_page` para que si se produce un error 404, redirija a `404.html`
  - Añade una directiva `error_page` para que si se produce un error 500, 502, 503 o 504 redirija a `50x.html`

Genera el archivo `docker-compose.yml` con la siguiente configuración:

- Versión 3.8
- Nombre del escenario: `ec4.3`
- Crear el servicio nombre `nginx` con las siguientes características:
  - contenedor nombre: `ec43_nginx`
  - indica que es un [contenedor interactivo](https://betterstack.com/community/questions/question-interactive-shell-using-docker-compose/)
    ```yaml	
    nginx:
      container_name: ec43_nginx
      ...
      # Estas opciones son para poder acceder al contenedor con un terminal interactivo en Docker-compose
      stdin_open: true
      tty: true
      command: bash
    ```
    para poder acceder a él. (Es igual a la opción `-it` de `docker exec`)
  - Usar el puerto 8001 del host y el puerto 80 del contenedor.
  - Montar el fichero de configuración `mypetshop.conf` con la nueva configuración aplicada en el directorio adecuado del contenedor.
  - Montar el directorio `app` en el directorio y nombre del mismo adecuado dentro contenedor
  

Configurar a través del plugin de Chrome [Awesome Host Manager](https://chromewebstore.google.com/detail/awesome-host-manager/pikaoeecieigblebdddckmlegonlogha?hl=es) la redirección de `mypetshop.local www.mypetshop.local` a `localhost:8001`.

> 📄 _Realiza las siguientes pruebas_
> 1. Acceder a través del navegador `mypetshop.local` y `www.mypetshop.local` y se visualiza la página web.
> 2. Permite visualizar el contenido (lista los archivos) de la carpeta `images` en la url `mypetshop.local/images`.
> 3. Si se accede a una página que no existe (`mypetshop.local/missing`) , se visualiza página `404.html`.
> 4. Si se produce un error 500 (accede a `mypetshop.local/500` para simular) se visualiza la página `50x.html`.

#### 🔧 **Solución de problemas**:

Para la solución de problemas, ten en cuenta los siguientes puntos:

- Si no funciona algo, revisa los logs de `error.log` de Nginx para ver si hay algún error en la configuración o en el acceso a los ficheros de la página web
- Si realizas cambios en la configuración, recarga la configuración de Nginx con el comando `nginx -s reload` dentro del contenedor, o para e inicia de nuevo el contenedor.


### Ejercicio 4.3.2: Logs personalizados

Un tema fundamental a la hora de poder monitorizar y solucionar problemas en un servidor web es el acceso a los logs. En este ejercicio vamos a configurar Nginx para que genere logs personalizados, con un formato específico, y un nivel de detalle determinado.

Para esto, modifica el archivo de configuración `mypetshop.conf` para que genere logs de acceso con el siguiente formato:

- Formato personalizado: `$remote_addr - $remote_user [$time_local] "$request" $status $body_bytes_sent "$http_referer" "$http_user_agent"`
- Nivel de detalle: `info`
- Ruta del fichero de logs:
  - access_log: `/var/log/nginx/mypetshop_access.log`
  - errpr_log: `/var/log/nginx/mypetshop_error.log`
  
- Rota el fichero de logs cada 10MB, manteniendo 5 ficheros de logs antiguos. (Usa la directiva `logrotate`)
- Añade una directiva `log_not_found` para que se registre en el log de errores cuando se produzca un error 404.
- Añade una directiva `log_format` para que se registre en el log de errores cuando se produzca un error 404.


Para probar esta nueva configuración, reinicia el contenedor, y revisar que los logs se generan correctamente. Para esto, sigue los siguientes pasos:

1. Abre 2 terminales (lado a lado) y accede al contenedor `ec43_nginx` (usando el comando `docker compose exec ec43_nginx bash`) en cada una de ellas.
2. En una de las terminales, ejecuta el comando `tail -f /var/log/nginx/mypetshop_access.log` para ver los logs de acceso.
3. En la otra terminal, ejecuta el comando `tail -f /var/log/nginx/mypetshop_error.log` para ver los logs de errores.

Ahora accede desde el navegador y realiza las mismas pruebas que en el punto 4.3.1. En los logs deberías ver las peticiones que se realizan, y los errores.

#### Cambiar el nivel de detalle de los logs

A veces nos interesa cambiar el nivel de detalle de los logs, para poder ver más información o menos. Para cambiar el nivel de detalle de los logs, sigue los siguientes pasos:

1. Cambia el nivel de detalle de los logs a `debug`, guarda la configuración y reinicia el servicio de Nginx (sin parar el contenedor)
2. Desde los terminales que tienes abiertos, comprueba que los logs de acceso y errores muestran más información.






