# Ejercicios 4.2

Para la realización de estos ejercicios, crea un nuevo directorio en tu repositorio llamado `UT4\EC4.2`

> 🔌 **Realiza los ejercicios con Docker**<br>
> - Para la realización de este ejercicio, usa la última versión de Nginx disponible en Docker Hub.
> - Estos ejercicios se realizarán dentro del contenedor de Docker

Este ejercicio trata de 2 partes:

1. Desplegar una página web en un servidor Nginx con Docker-compose
2. Crear una imagen de docker, que contenga la configuración.
3. Desplegar la el servidor Nginx con la imagen creada.

### Ejercicio 4.2.1 Despliegue con Docker-compose

Basado en el ejercicio 4.1, vamos a desplegar una página web estática, con un dominio asociado `mypetshop.local` en un servidor Nginx con Docker-compose.

> 🏷️ 
Los ficheros de la página están disponible en el siguiente enlace [Mypetshop](./res/mypetshop.website.zip).

Para esto crea la siguiente estructura de directorios:

```plaintext
UT4\EC4.2
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

```nginx
server {
    listen 80;
    server_name mypetshop.local;
    root /usr/share/nginx/html;
    index index.html;
}
```

Genera el archivo `docker-compose.yml` con la siguiente configuración:

- Versión 3.8
- Nombre del escenario: ec4.2
- Crear el servicio nombre `nginx` con las siguientes características:
  - Usar el puerto 8001 del host y el puerto 80 del contenedor.
  - Montar el fichero de configuración `mypetshop.conf` en el directorio adecuado del contenedor.
  - Montar el directorio `app` en el directorio y nombre del mismo adecuado dentro contenedor
  

Configurar a través del plugin de Chrome [Awesome Host Manager](https://chromewebstore.google.com/detail/awesome-host-manager/pikaoeecieigblebdddckmlegonlogha?hl=es) la redirección de `mypetshop.local www.mypetshop.local` a `localhost:8001`.


### Ejercicio 4.2.2 Crear imagen de Docker

Una vez hemos probado la configuración, vamos a crear una imagen de Docker que contenga la configuración y página web del ejercicio anterior.

Para esto, agregar un archivo `Dockerfile` en el directorio `UT4\EC4.2` con la siguiente configuración:

- Basado en la versión de nginx:1.25.3-alpine
- Copiar el fichero `mypestshop.conf` en el directorio correcto del contenedor.
- Copiar el directorio `app` con el nombre `mypetshop.local` en el directorio correcto del contenedor, según la configuración del fichero `mypetshop.conf`.
- Exponer el puerto 80 del contenedor.
- Como línea final indicar el comando para que se inicie Nginx al arrancar un contenedor badado en esta imagen `CMD ["nginx", "-g", "daemon off;"]`


Una vez creado el `Dockerfile`, construye la imagen con el nombre `ec42/mypetshop` y la etiqueta `v1`.



### Ejercicio 4.2.3 Despliegue con la imagen creada

Una vez creada la imagen, vamos a desplegar un contenedor con la imagen creada.

Sigue los siguientes pasos:

1. crea un contenedor con el nombre `ec42_mypetshop` a partir de la imagen `ec42/mypetshop:v1` y que escuche en el puerto 8001 del host y el puerto 80 del contenedor.
2. Accede a través del navegador a la dirección `mypetshop.local` y `www.mypetshop.local` y comprueba que la página web está disponible, y que el contenido es el mismo que el desplegado en el ejercicio 4.2.1.




