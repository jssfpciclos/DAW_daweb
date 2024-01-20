# UT2-TE3.1: Implantación de arquitecturas web

### TAREA EVALUABLE

1. Implantar una aplicación PHP que funcione como una calculadora usando Nginx + PHP-FPM.
2. Realizar el despliegue en la máquina local con la url http://localhost para instalación con 2 contenedores **entorno dockerizado** (docker-compose con imagen incluya PHP-FPM).

### Entregable

Informe explicando los pasos según se indica en el [punto](#explicación-de-la-tarea) seguidos para resolver la tarea.
El informe se entregará en un fichero `README.md` en el repositorio oficial del alumno, en la carpeta `UT3/TE3.1/`.<br>

Se entregará un PDF (en moodle) con el siguiente formato:

1. Titulo de la tarea, donde se indique el nombre de la tarea y el nombre de la asignatura, y el nombre del alumno, asi como el enlace (formato commit) al fichero (README.md) de vuestro repositorio.

## Aplicación PHP

1. Utilizar una interfaz similar a la siguiente:

![Plantilla](images/template.png)

2. Incluir [esta imagen de la calculadora](./images/calculadora.png).
3. Incluir un fichero `.css` con unos estilos básicos.

### Estructura de directorios

```
UT3\TE3.1
├── app
│   ├── calculadora.php
|   ├── images
│   │   └── calculadora.png
│   ├── index.php
│   └── styles.css
├── config
│   └── default.conf
├── dockerfile
├── docker-compose.yml

```

**Nombres de las imágen:** `iessdf/calculadora-php-nativa`


## Explicación de la tarea

- Explica cada uno de los pasos realizados para la realización de la tarea.
- Los pasos deben estar numerados, y con explicación de qué se hace en ese paso, y si es requerido incluir imagen para su comprensión (INCLUIRLA).
- Para el docker-compose, explicar con comentarios dentro del fichero docker-compose.yml cada uno de los pasos realizados.
  
  Ejemplo
  ```yml
  version: '3.7'
  services:
    # Servicio web, pongo el nombre `web`
    web:
      # Imagen que voy a utilizar. Utilizo la versión 8.0 de nginx, con sistema operativo alpine
      image: nginx:8.0-alpine
      # Nombre del contenedor que se va a crear
      container_name: web
      # puerto que se mapena. 80 del contenedor a 80 de la máquina local
      ports:
        - 80:80
      # Volumen que se va a utilizar. Se mapea la carpeta app del directorio actual a la carpeta /usr/share/nginx/html del contenedor
      volumes:
        - ./app:/usr/share/nginx/html
      ...
  ```

  ### 💡 Paso final

  Como paso final, incluir un gif animado con la ejecución de la calculadora dentro del navegador, donde se vea la URL (localhost) y el funcionamiento de la calculadora. *Hacer el navegador pequeño para que se vea la URL y la calculadora*


   