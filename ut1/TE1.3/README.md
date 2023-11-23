# UT1-TE1.3: Documentación y sistemas de control de versiones

### Recursos
 
- [Como hacer tu primera Pull Request en un proyecto GITHUB 🧱](https://youtu.be/_M8oalUyz10)
- [Documentación de la Unidad de Trabajo](https://sharp-voice-0ff.notion.site/Documentaci-n-y-sistemas-de-control-de-versiones-4f34a299f66d42b1aac4853788a41127)
  - Revisar especificamente el punto "Escenarios de colaboración > Colaborando "Open Source". (final del documento)

### TAREA EVALUABLE 1.3

1. El alumnado trabajará por parejas: `user1` y `user2`. Indicar quién es `user1` y quién es `user2`.
2. `user1` creará un **repositorio público** llamado **git-work** en su cuenta de GitHub, añadiendo un `README.md` y una licencia MIT.
3. `user1` clonará el repo y añadirá los ficheros: [index.html](./files/index.html), [bootstrap.min.css](./files/bootstrap.min.css) y [cover.css](./files/cover.css). Luego subirá los cambios al remoto `origin` (_upstream_).
4. `user2` creará un fork de **git-work** desde su cuenta de GitHub.
5. `user2` clonará su fork del repo.
6. (No-hacer)
7. `user2` creará una nueva rama `custom-text` y modificará el fichero `index.html` personalizándolo para una supuesta startup.
   Subirá los cambios al remoto `origin`. (`git push origin`)
8. `user2` enviará un pull-request (PR) a `user1` (marcando `Allow edits from maintainers`).
9. `user1` probará el PR de `user2` en su máquina (copia local):
   -  Agregando un remoto de nombre `origin-forked` y la rama `custom-text` del `user2` (`git remote add origin-forked {url-repositorio-fork}`)
   -  Obtienendo los últimos cambios del remoto (`git fetch origin-forked custom-text`), sin mezclarlos con su copia local.
   -  Cambiar a rama `custom-text`. (`git checkout custom-text`)
   -  Y realizar ciertos cambios en su copia local. (Cambiar cualquier texto en `index.html`)
   -  Una vez los cambios realizados en local, subir los cambios al remoto `git push origin-forked`.
10. `user1` y `user2` tendrán una pequeña conversación en la página del PR, donde cada usuario incluirá, al menos, un cambio más.
11. `user1` finalmente aprobará el PR.
12. `user1` actualizará la rama principal en su copia local. (`git pull origin main`)
    > (Es importante ahora eliminar el remoto `origin-forked` y la rama `custom-text` de su copia local.)
    ```bash	
    git remote remove origin-forked
    git branch -d custom-text
    ```

13. `user2` incorporará los cambios del `user1` rama main (a través de la interfaz de Github). 
    Ahora, los cambios que envió `user2` en el PR, se encuentran en la rama `main` de `user1`, y ahora también en la rama `main` de `user2`.<br>

    == POR TANTO EL CICLO SE HA CERRADO ==

14. `user2` deberá actualizar su copia local desde remoto en su rama `main`. (`git pull origin`)
    
#### Ejecutar limpieza de ramas

Ahora que `user2` ha incorporado los cambios en la rama `main` de `user1` en su rama principal, puede eliminar la rama `custom-text` de su repositorio local y remoto.

15. `user2` eliminará la rama `custom-text` de su repositorio local y remoto.
    > Fundamental, posicionarse en otra rama distinta a la que se va a eliminar. (Ej: `main`)

        - `git branch -d custom-text` (local)
        - `git push origin --delete custom-text` (remoto)
    


## Entregable

Informe explicando los pasos seguidos para resolver la tarea. Las dos personas de cada pareja deberán subir el mismo informe y la calificación será la misma para ambas.

⚡ Revisa las [instrucciones sobre entrega de tareas](../../_info/entrega-tareas-info.md).
