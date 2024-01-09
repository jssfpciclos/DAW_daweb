# Servidores Web

**Recursos**

Texto:
- [Nginx](https://www.nginx.com/)
  - [Nginx Docs](https://nginx.org/en/docs/)
  - [Directivas](https://nginx.org/en/docs/dirindex.html)

Videos:

- OpenWebinars: 
  - [Laboratorio de introducción a la administración de servidores web](https://openwebinars.net/academia/aprende/admin-sistemas-nginx-introduccion/)
  


Un servidor web es un programa que se ejecuta en un servidor y que se encarga de procesar las peticiones que llegan desde los clientes. Estas peticiones pueden ser de varios tipos, pero la más común es la petición de un archivo HTML, que es lo que se envía al navegador para que lo muestre al usuario.

Los servidores web más comunes son Apache, Nginx, IIS y LiteSpeed. En este artículo vamos a centrarnos en Apache y Nginx, que son los más utilizados.


## Apache vs Nginx

Apache y Nginx son dos servidores web muy potentes y con muchas opciones de configuración. A continuación vamos a ver las principales diferencias entre ambos servidores web.

|  |APACHE	|NGINX	  | LITESPEED   |
| --- | --- | --- | --- |
|código	  |abierto	  |  abierto	| abierto	 |
|arquitectura	  | módulos	 | eventos	 | eventos |
|rendimiento	  | bajo por sí solo |buen rendimiento  |  mayor que el resto|
|soporte	| propio | externo | propio|
| compatiblidad| Windows,Unix|Windows,Unix|Windows,Unix|

Son muy diferentes.

Hay que entender que Apache fue el primer servidor HTTP y, durante muchos años, no hubo alternativa. Por lo tanto, es un proyecto mucho más maduro y que ha conseguido estandarizar ciertas cosas a las que actualmente están acostumbrados casi todos los webmasters, como el uso del .htaccess.

Nginx, por su parte, es un proyecto mucho más joven y que ha sido desarrollado con el objetivo de mejorar el rendimiento de Apache. Por lo tanto, es un servidor web mucho más ligero y que consume menos recursos que Apache.

## Nginx

Nginx es un servidor web ligero y de alto rendimiento. Es de código abierto, lo que facilita la personalización. Es muy popular y, junto con Apache, gobiernan prácticamente todo el mercado de servidores web.

El desarrollo de Nginx comenzó en 2002 cuando surgió la necesidad de aumentar el número de solicitudes simuladas por servidor.

A nivel técnico, un servidor Nginx utiliza una arquitectura de subproceso asíncrono. Esto significa que cuando se genera una solicitud, no crea un nuevo proceso en el procesador del servidor, aumentando así el rendimiento del servidor.

Nginx es un servidor web que se utiliza para servir contenido estático y dinámico en la web. También se puede utilizar como proxy inverso, balanceador de carga y proxy de correo electrónico para protocolos IMAP, POP3 y SMTP.

A diferencia de Apache, nginx no se basa en procesos sino en eventos. Las solicitudes individuales se clasifican moco eventos y se procesan de forma asíncrona. Esto permite que nginx maneje un gran número de solicitudes simultáneas con un uso mínimo de recursos.

La cantidad de procesos existentes y la manera en la que se dividen las solicitudes del servidor (es deicr, los eventos) se definen en el archivo de configuración de nginx. Este archivo se encuentra en /etc/nginx/nginx.conf. En este archivo se definen los parámetros de configuración del servidor, como el número de procesos, el número de eventos, el usuario que ejecuta el servidor, etc.


#### Directorios y ficheros

- `/etc/nginx` - carpeta raiz para la configuración por defecto para el servicio NGINX
  * otras rutas: `/usr/local/etc/nginx`, `/usr/local/nginx/conf`

- `/etc/nginx/nginx.conf` - es la configuración principal para el servicio NGINX, incluye el bloque máximo-nivel http y todas las otras configuraciones y files
  * otras rutas: `/usr/local/etc/nginx/nginx.conf`, `/usr/local/nginx/conf/nginx.conf`

- `/usr/share/nginx` - es el directorio raíz predeterminado para solicitudes, contiene el directorio `html` y archivos estáticos básicos
  * otras rutas: `html/` es el directorio raíz

- `/var/log/nginx`: es la ubicación predeterminada del log (log de acceso y errores) para NGINX
   * otras rutas: `logs/` en el directorio raíz

- `/var/cache/nginx`: es la ubicación predeterminada de los archivos temporales para NGINX
   * otras rutas: `/var/lib/nginx`

- `/etc/nginx/conf` - contiene archivos de configuración personalizados/vhosts
   * otras rutas: `/etc/nginx/conf.d`, `/etc/nginx/sites-enabled` (no soporto esta convención similar a Debian/Apache)

- `/var/run/nginx`: contiene información sobre los procesos NGINX
   * otras rutas: `/usr/local/nginx/logs`, `logs/` en el directorio raíz


#### Comandos

  >💡 Es posible recargar la configuración de NGINX sin reiniciar el servicio: `nginx -s reload`

- `nginx -h` - muestra la ayuda
- `nginx -v` - muestra la versión de NGINX
- `nginx -V`: muestra información ampliada sobre NGINX: versión, parámetros de compilación y argumentos de configuración.
- `nginx -t` - prueba la configuración de NGINX
- `nginx -c <nombre de archivo>` - establece el archivo de configuración (predeterminado: `/etc/nginx/nginx.conf`)
- `nginx -p <directorio>` - establece la ruta del prefijo (predeterminado: `/etc/nginx/`)
- `nginx -T` - prueba la configuración de NGINX e imprime la configuración validada en la pantalla
- `nginx -s <señal>` - envía una señal al proceso maestro NGINX:
   - `stop`: interrumpe el proceso NGINX inmediatamente
   - `quit`: detiene el proceso NGINX una vez que termina de procesarse
solicitudes a bordo
   - `reload` - recarga la configuración sin detener los procesos
   - `reabrir`: indica a NGINX que vuelva a abrir los archivos de registro
- `nginx -g <directiva>` - establece [directivas globales](https://nginx.org/en/docs/ngx_core_module.html) fuera del archivo de configuración


Algunos útiles snippets de configuración de NGINX:

```nginx
# testing configuration
nginx -t -c /etc/nginx/nginx.conf

# starting daemon
service nginx start # or systemctl start nginx

# stopping daemon
service nginx stop # or systemctl stop nginx

# restarting daemon
service nginx restart # or systemctl restart nginx

# reloading configuration
ngixn -s reload
```

#### Configuración

NGINX usa un micro lengua de configuración, que es muy flexible y fácil de aprender. La configuración de NGINX se divide en bloques, que se pueden anidar. Cada bloque comienza con una llave de apertura `{` y termina con una llave de cierre `}`. Los bloques se pueden anidar, pero no se pueden superponer.

> 💡 Comentarios:
>  - NGINX no es sensible a mayúsculas y minúsculas, por lo que `server_name` y `Server_Name` son lo mismo.
>  - La configuración no soporte los bloques de comentarios, solo los comentarios de una línea que comienzan con `#`.
> - Lineas que contengan directivas de configuración deben terminar con un punto y coma `;` (de otra manera, NGINX lanzará un error).
> - Variables,Strings y valores booleanos no necesitan comillas, pero si se usan, deben ser comillas simples `'` o dobles `"`.

##### Directivas

Las directivas son las instrucciones que se utilizan para configurar NGINX. Las directivas se pueden agrupar en bloques. Cada directiva tiene un nombre y un valor, separados por un espacio. El valor puede ser una cadena, un número, un booleano o una lista de valores separados por espacios.

Técnicamente, todo dentro de NGINX es una directiva. Son de 2 tipos:

- Directivas simples: son directivas que tienen un nombre y un valor. 
  
```nginx
# directive
directive value;
```
- Directivas de bloque: son directivas que tienen un nombre y un bloque de configuración.
  - Pueden contener otras directivas y bloques.
  - Una directiva de bloque que contiene otras directivas y bloques se llama `bloque de contexto`.

```nginx
# directive block
directive {
  # ...
}
```

##### Bloques

Los bloques son la base de la configuración de NGINX. Los bloques se pueden anidar, pero no se pueden superponer. Cada bloque comienza con una llave de apertura `{` y termina con una llave de cierre `}`.

```nginx
# block
block {
  # nested block
  block {
    # ...
  }
}
```

##### Contextos

Los contextos son los bloques en los que se pueden colocar las directivas. NGINX tiene varios contextos, que se utilizan para configurar diferentes aspectos del servidor. Los contextos más comunes son `http`, `server` y `location`.

```nginx
# context
http {
  listen 80;
  server {
    # ...
  }
}
```

Hay 4 contextos principales en NGINX:

- `events`: contiene directivas que se aplican a eventos de conexión.
- `http`: contiene directivas que se aplican a conexiones HTTP.
- `server`: contiene directivas que se aplican a un servidor virtual.
- `location`: contiene directivas que se aplican a una ubicación específica.

- `main`: contiene directivas que se aplican a todo el servidor.

> ✏️ **Contextos**: Un contexto se puede comparar como ámbitos en los lenguajes de programación. Las directivas que se encuentran dentro de un contexto se aplican a ese contexto. Por ejemplo, las directivas que se encuentran dentro del contexto `http` se aplican a todas las conexiones HTTP.

##### Variables

Las variables se utilizan para almacenar valores que se pueden utilizar en la configuración. Las variables se definen con el signo `$` y se pueden utilizar en cualquier lugar de la configuración.

```nginx
# variable
set $variable value;
```

#### Ejemplo de configuración

```nginx
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

## Sirviendo contenido estático

NGINX además de muchas otras cosas, es un servidor web. Por lo tanto, puede servir contenido estático, como archivos HTML, CSS, JavaScript, imágenes, etc.

Para servir contenido estático, debe definir un bloque `server` en el archivo de configuración de NGINX. El bloque `server` define la configuración para un servidor virtual.

> 💡 **Servidor virtual**: Un servidor virtual es un servidor que se ejecuta en el mismo servidor físico que otros servidores virtuales, pero que se comporta como un servidor independiente.

En la configuración siguiente, definimos un servidor virtual que escucha en el puerto 80 y que sirve archivos estáticos desde el directorio `/var/www/example.com`.

```nginx
server {
  listen 80;
  server_name example.com www.example.com;

  root /var/www/example.com;
  index index.html;
}
```
Si diseccionamos la configuración anterior, podemos ver lo siguiente:

- En el bloque `server` definimos dos directivas: `listen` y `server_name`.

- La directiva `listen` define el puerto en el que escucha el servidor virtual. En este caso, el servidor virtual escucha en el puerto 80, que es el puerto predeterminado para HTTP.

- La directiva `server_name` define el nombre del servidor virtual. En este caso, el servidor virtual responde a las solicitudes que coinciden con los nombres `example.com` y `www.example.com`.

- En el bloque `server` definimos dos directivas: `root` e `index`.
  - La directiva `root` define el directorio raíz del servidor virtual. En este caso, el directorio raíz es `/var/www/example.com`.
  - index define el archivo que se sirve cuando se solicita el directorio raíz. En este caso, el archivo que se sirve es `index.html`.


**Bloque location**

El bloque `location` se utiliza para definir la configuración para una ubicación específica. La ubicación puede ser un archivo o un directorio. En el siguiente ejemplo, definimos un bloque `location` que define la configuración para el archivo `robots.txt`.

```nginx
server {
  listen 80;
  server_name example.com www.example.com;

  root /var/www/example.com;
  index index.html;

  location /robots.txt {
    alias /var/www/example.com/robots.txt;
  }
}
```

Si no se especifica una directiva `location` para un archivo o directorio, se utiliza la configuración del bloque `server`. En este caso, cualquier carpeta o archivo que no tenga una directiva `location` definida se sirve desde el directorio raíz del servidor virtual.

Si diseccionamos la configuración anterior, podemos ver lo siguiente:

- En el bloque `location` definimos una directiva: `alias`.
  - La directiva `alias` define la ruta del archivo que se sirve cuando se solicita la ubicación `/robots.txt`. En este caso, el archivo que se sirve es `/var/www/example.com/robots.txt`.
  

**Bloque location con expresiones regulares**

El bloque `location` también se puede utilizar con expresiones regulares. En el siguiente ejemplo, definimos un bloque `location` que define la configuración para todos los archivos que terminan con `.txt`.

```nginx
server {
  listen 80;
  server_name example.com www.example.com;

  root /var/www/example.com;
  index index.html;

  location ~ \.txt$ {
    alias /var/www/example.com/robots.txt;
  }
}
```

## Servir contenido dinámico



