# Entrega de tareas

La entrega de las tareas se hará vía **repositorio de GitHub**.

## Creación del repositorio

Debes crear un **repositorio privado** en GitHub con el nombre **`2324_DAWeb_{NombreApellido1}`** y dar permisos de lectura al usuario `jssdocente`.

## Estructura del repositorio

```python
ut1
 └─ te1.1
 └─ te1.2
 └─ ...
ut2
 └─ te2.1
 └─ te2.2
 └─ ...
...
```

> 💡 UT viene de Unidad de Trabajo y BT viene de Boletín/Tarea Evaluable.

## Contenido de la Tarea Evaluable

Dentro de cada carpeta `te<X>` el contenido será el siguiente:

- `screenshots`: carpeta para capturas de pantalla.
- `src`: carpeta para código de aplicación (si procede).
- `images`: carpeta para otras imágenes (si procede).
- `README.md`: informe escrito en GitHub sabor Markdown.

Los "`h1`" (`# <Heading>`) del `README.md` deberán **coincidir con los criterios a evaluar de la rúbrica** correspondiente a la tarea y habrá que **crear un índice** a estos epígrafes al principio del informe.

## Comandos

Los informes que incluyan **comandos en terminal**, estos habrán de **tomarse como capturas de pantalla** donde se vea suficientemente grande el texto de los comandos.

Habrá que incluir **tanto el comando como su salida**.

**No es necesario poner el comando "en texto"** antes de la captura de pantalla, basta con la propia captura de pantalla que ya incluye el comando y su salida.

## URLs

Si la tarea incluye acceso a cualquier URL, la **captura de pantalla** deberá incluir la **barra de direcciones** del navegador.

## Apuntes

No se trata de copiar el contenido de los apuntes tal cual en el informe. Habrá cosas que harán falta y otras que no. **El objetivo es crear una historia ordenada** que tenga sentido y que transmita la sensación de haber comprendido el proceso global.

## Subida de la tarea

Se habilitará una entrega en el **Moodle** donde se tendrá que subir únicamente la URL al `README.md` incluyendo el commit específico.

Para ello basta con acceder en GitHub al fichero en cuestión:

→ `https://github.com/<user>/<repositorio>/blob/main/ut1/te1/README.md`

, y pulsar la tecla <kbd>y</kbd> para que la URL se nos convierta en un formato tipo:

→ `https://github.com/<user>/dpl/blob/ffaabb62206fa0c0f350dfe0a4ba370ed00b9218/ut1/te1/README.md`

> 💡 La parte de la url que consta de 40 caracteres es el **hash del commit** y lo identifica de manera unívoca: `ffaabb62206fa0c0f350dfe0a4ba370ed00b9218`

Por lo tanto, **lo único que hay que subir es la URL que incluye el commit**.
