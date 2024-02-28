# UT6. Tarea Evaluable 6.2 - Desplegar con Docker a Digital Ocean

### Alcance

Este tarea se basa en el [ejercicio](../EC/6.2/readme.md) trata de 4 partes:

1. Crear y configurar un sevidor Ubuntu en Digital Ocean a través de un Droplet.
2. Configurar SSH, Firewall, Nginx y PHP en el servidor.
3. Desplegar la aplicación PHP en el servidor.
4. Desplegar una web estática bajo un dominio.


### 📝 Entregable

La documentación se entregará en un fichero `README.md` en el repositorio oficial del alumno, en la carpeta `UT6/TE6.2/`.<br>

Se entregará además un PDF (en moodle) con el siguiente formato:

- Titulo de la tarea, donde se indique el nombre de la tarea y el nombre de la asignatura
- Nombre del alumno
- Enlace en formato commit


#### Estructura de entrega

La estructura del documento será la siguiente:

- Titulo de la tarea, donde se indique el nombre de la tarea y el nombre de la asignatura
- Nombre del alumno
- Descripción breve de en qué consiste la tarea y el objetivo de la misma.
- Cada punto de la tarea, debe tener una explicación de porqué se hace eso, y explicación de los pasos realizados.


### 📋 Tarea

La tarea consiste en desplegar una aplicación estática a través de un Docker en Digital Ocean.

![alt text](img/01.concepto.png)


  
  

#### 6.2.1 Explicación del proceso

> 📄 En este apartado debes explicar la práctica, qué pasos hay que realizar para poder conseguir tener desplegada nuestra App en Internet.



#### 6.2.2 Estructura de carpeta para crear el DockerFile

> 📄 Explicar porqué la estrucutra de carpetas que has realizado, y para qué se utiliza cada fichero

> 🧲 Adjunta capturas de pantalla donde se visualize la estrucutra de carpetas


#### 6.2.3 Creación del DockerFile

> 📄 Explicar el contenido del DockerFile, qué pretendes con él y explicación de las intrucciones que lo conforman

> 🧲 Adjunta capturas de pantalla donde se visualize la estrucutra de carpetas


#### 6.2.2(0) Configuración del servidor, Instalación de Nginx y PHP

> 🧲 Adjunta capturas de pantalla donde se vea la instalación de Nginx y PHP en el servidor.
> - Versión de Nginx 1.23.4, Versión de PHP-FPM, y estado de todos los servicios instalados.



#### 6.2.2(1) Configuración del servidor, Instalación de Nginx y PHP


> Adjunta capturas de pantalla donde resaltes y expliques que tienes que cambiar en la configuración de PHP-FPM y Nginx para que funcione la integración entre ambos servicios.


#### 6.2.2(2) Probar configuración de PHP

Crea una página `info.php` en el directorio `/usr/share/nginx/html` para que muestre la información de PHP.

> 🧲 Adjunta una captura de pantalla donde se vea la información de PHP en el navegador y la IP del servidor.



#### 6.2.3 Despleguar aplicación PHP

En este paso despliega una aplicación PHP en el servidor, con los siguientes requisitos:

- Borra la página `info.php` que has creado anteriormente, y el fichero `index.html` que viene por defecto.
- Clona el siguiente [repositorio](https://github.com/ZeshanWD/php-site.git) en la carpeta `/usr/share/nginx/html`.
- Cambia la configuración por defecto de Nginx (default.conf) para que el fichero `index.php` sea el único fichero por defecto.
- Crea una página de error personalizada para el código 404, que muestre un mensaje personalizado. (Haz una tu de forma muy sencilla)
- Realiza cualquier cambio necesario para que la aplicación funcione correctamente.

> 🧲 Adjunta lo siguiente:


1. Fichero de configuración `default.conf` de Nginx.
   ```nginx
   ```	

2. GIF donde se vea el acceso a la aplicación PHP en el navegador, y navegación por la web. También realizar acción para que se muestre la página de error 404.



#### 6.2.4 Configurar un Virtual Host

Según como se indica en este [punto](../EC/6.2/readme.md#configurar-nginx-para-el-dominio) configura un dominio para la web `petshop.ddns.net` como se indica en el ejercicio, anteponiendo tus iniciales al nombre del dominio.

Para ello, utiliza el código fuente de la web [Mypetshop](../../../UT4/EC/res/mypetshop.website.zip).


> 🧲 Adjunta lo siguiente:

1. Captura de la pantalla configuración NoIP donde se visualice la vinculación del dominio `petshop.ddns.net` con la IP pública del servidor.

2. Fichero de configuración `default.conf` de Nginx.

3. GIF donde se vea el acceso a la aplicación a la Web en el navegador utilizando el dominio `petshop.ddns.net` y navegación por la web. Fuerza también a utilizar un error para que se muestre la página 404.