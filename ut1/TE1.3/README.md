# UT1-TE1.3: Documentación y sistemas de control de versiones

### Recursos
 
- [Como hacer tu primera Pull Request en un proyecto GITHUB 🧱](https://youtu.be/_M8oalUyz10)
- [Documentación de la Unidad de Trabajo](https://sharp-voice-0ff.notion.site/Documentaci-n-y-sistemas-de-control-de-versiones-4f34a299f66d42b1aac4853788a41127)

### TAREA EVALUABLE 1.3

1. El alumnado trabajará por parejas: `user1` y `user2`. Indicar quién es `user1` y quién es `user2`.
2. `user1` creará un **repositorio público** llamado **git-work** en su cuenta de GitHub, añadiendo un `README.md` y una licencia MIT.
3. `user1` clonará el repo y añadirá los ficheros: [index.html](./files/index.html), [bootstrap.min.css](./files/bootstrap.min.css) y [cover.css](./files/cover.css). Luego subirá los cambios al _upstream_.
4. `user2` creará un fork de **git-work** desde su cuenta de GitHub.
5. `user2` clonará su fork del repo.
6. `user1` creará una issue con el título "Add custom text for startup contents".
7. `user2` creará una nueva rama `custom-text` y modificará el fichero `index.html` personalizándolo para una supuesta startup.
8. `user2` enviará un pull-request (PR) a `user1` (marcando `Allow edits from maintainers`).
9. `user1` probará el PR de `user2` en su máquina (copia local), clonando el repositorio del `user2` en un nueva carpeta, posicionandose en la rama `custom-text`, y realizará ciertos cambios en su copia local que luego deberá subir al propio PR (usando `git push` a la rama `custom-text` en remoto).
10. `user1` y `user2` tendrán una pequeña conversación en la página del PR, donde cada usuario incluirá, al menos, un cambio más.
11. `user1` finalmente aprobará el PR, cerrará la issue creada (usando una referencia a la misma) y actualizará la rama principal en su copia local.
12. `user2` deberá incorporar los cambios de la rama principal de `upstream` en su propia rama principal.
13. `user1` creará una issue con el título "Improve UX with cool colors".
14. `user1` cambiará la línea 10 de `cover.css` a:

```css
color: purple;
```

12. `user1` hará simplemente un commit local en main → NO HACER `git push`.
13. `user2` creará una nueva rama `cool-colors` y cambiará la línea 10 de `cover.css` a:

```css
color: darkgreen;
```

14. `user2` enviará un PR a `user1`.
15. `user1` probará el PR de `user2` (en su copia local). A continuación tratará de mergear el contenido de la rama `cool-colors` en su rama principal y tendrá que gestionar el conflicto: Dejar el contenido que viene de `user2`.
16. Después del commit para arreglar el conflicto, `user1` modificará la línea 11 de `cover.css` a:

```css
text-shadow: 2px 2px 8px lightgreen;
```

16. `user1` hará un commit especificando en el mensaje de commit el cambio hecho (sombra) y que se cierra la issue creada (usar referencia a la issue). A continuación subirá los cambios a `origin/main`.

17. `user1` etiquetará esta versión (en su copia local) como `0.1.0` y después de subir los cambios creará una "release" en GitHub apuntando a esta etiqueta.

## Entregable

Informe explicando los pasos seguidos para resolver la tarea. Las dos personas de cada pareja deberán subir el mismo informe y la calificación será la misma para ambas.

⚡ Revisa las [instrucciones sobre entrega de tareas](../../_info/entrega-tareas-info.md).
