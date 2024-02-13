# Ejercicios 4.1

Para la realización de estos ejercicios, crea un nuevo directorio en tu repositorio llamado `UT4\EC4.1` y copia en él el archivo `EC4.1_ejercicios.md`.

> 🔌 **Realiza los ejercicios con Docker**<br>
> - Para la realización de este ejercicio, usa la última versión de Nginx disponible en Docker Hub.
> - Estos ejercicios se realizarán dentro del contenedor de Docker

### Ejercicio 4.1.1

Indica los comandos necesarios para realizar las siguientes tareas, en los huecos habilitados para ello:

1. Instalar nginx de forma natia en un sistema Ubuntu/debian.
   ```bash
    
    ```
2. Verificar si Nginx está instalado <br>
   *Explica cómo verificar si Nginx está instalado en tu sistema.*
   ```text
    
    ```
3. Realiza las siguientes tareas:
   - Iniciar el servicio.
      ```bash
      
      ```
    - Detener el servicio.
      ```bash
    
       ``
    - Recargar la configuración estando el servicio en ejecución.
      ```bash
    
      ```

4. Realiza las siguientes acciones a través de comandos, en el orden que se indica:
      ```bash
      # 1. accede al directorio donde está instalado Nginx.

      # 2. muestra el contenido en forma detallada del directorio.

      # 3. muestra el contenido del archivo con el comando `cat`.

      # 4. acceder a directorio donde están los archivos de log.

      # 5. muestra el contenido en forma detallada del directorio.

      # 6. Ubicación ruta archivos de la página web por defecto (comando grep).

      ```

5. Cambia el puerto por defecto de Nginx al puerto 8080, realiza todos los pasos a través de comandos, y utiliza el programa `vi` para editar el archivo de configuración.
   ```bash
    
    ```

6. Comprueba que la configuración de Nginx es correcta a través de una herramienta que proporciona el propio Nginx.
  
   - Realiza la comprobación sencilla
   ```bash
    
    ```

  - Realiza la comprobación completa
    ```bash
      
    ```
  - Realiza la comprobación completa, pero paginando el resultado.
    ```bash
      
    ```

7. Realiza desde dentro del servidor (localhost) una petición a la página web por defecto de Nginx, utilizando el puerto modificado con eo comando `curl`.
    ```bash
      
    ```

### Ejercicio 4.1.2

Nginx trae una configuración para un sitio-web por defecto, ubicado en el archivo `/etc/nginx/conf.d/default.conf`.

1. Renombra el archivo `default.conf` a `default.conf.no` para que no se aplique la configuración por defecto.
   ```bash
    # Renombra el archivo default.conf

    # Recarga la configuración de Nginx
    
    # Prueba que la página web por defecto ya no está disponible.

    ```

2. Ahora vamos a configurar un nuevo sitio web, para el sitio `mypetshop.local` con la siguiente configuración:
   - Assets ubicandos en el directorio `/var/www/mypetshop.local`.
   - Estará disponible en los dominios `mypetshop.local` y `www.mypetshop.local`.
   - Tendrá como página principal `index.html`.

   Realiza las siguientes tareas:
   - Crea el directorio `/var/www/mypetshop.local`.
   - Crea un archivo `index.html` en el directorio `/var/www/mypetshop.local` con el texto `site comming soon`.
   - El servidor debe estar disponible en el puerto 80.
   - Crea un nuevo archivo de configuración llamado `mypetshop.local.conf` en el directorio `/etc/nginx/conf.d/` que configure el nuevo sitio web.:
 
   Una vez realizadas las tareas, recarga la configuración de Nginx y comprueba que el sitio web está disponible.

   Para simular el dominio `mypetshop.local` en tu sistema (servidor), añade la siguiente línea al archivo `/etc/hosts`, a través del comando `tee` o `echo`:
   ```bash
    # Añade la siguiente línea al archivo /etc/hosts
    echo "127.0.0.1 mypetshop.local www.mypeteshop.local" | tee --append /etc/hosts

    # Prueba que el dominio mypetshop.local está disponible.
    curl mypetshop.local
    ```
  El resultado de la petición debe ser el contenido del archivo `index.html` que has creado.
   


3. Modifica el archivo de configuración `mypetshop.local.conf` con los siguientes cambios:
    - El sitio web estará disponible en el puerto 8080.
    - El sitio sea el servidor por defecto.
    - Si no se indica nada ninguna página, se redirija a `index.html`, sino a `index.htm` o `index.php`, en ese orden.

   Pasos:
   ```bash
    # Muestra el fichero de configuración modificado

    # Comprueba que la configuración es correcta con comandos de Nginx.
    
    # Recarga la configuración de Nginx

    # Pruebas las siguientes peticiones:
    
    # > curl mypetshop.local:8080

    # Renombra el archivo index.html a index.htm

    # > curl mypetshop.local:8080

    # Renombra el archivo index.htm a index.php

    # > curl mypetshop.local:8080
    ```

    En todos los casos, el resultado de la petición debe ser satisfactorio.

   

   