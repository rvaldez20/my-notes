# Notes de GIT

---

## Comandos de GIT

### Flujo de Git:
**Inicializa un repositorio**
Considera que es necesario estar en el directorio donde se va a crear el repositorio de git.
```git init ```

**Verificar el estado de los archivos**
Permite conocer el estatus de los diferentes archivos: nuevos, modificados, eliminados. Mostrará los archivos de diferentes colores según el estatus de los archivos. De color rojo (archivos nuevos, eliminados y modificados), color verde (archivos en área de preparación).

```git status ```

**Añadir archivos al área de preparación**
Mueve el estatus de los archivos del área local al área de preparación, se puede hacer de forma individual especificando ruta y nombre del archivo:

```git add _nombre_archivo_ ```

Y también se puede hacer utilizado un punto (.), con esto pasara todos los archivos a los que no se les está dando seguimiento.

```git add . ```

Incluso se puede hacer utilizando los comodines para seleccionar determinados archivos según su extensión, por ejemplo, el siguiente comando solo agregara los archivos con extensión HTML que no se les esté dando seguimiento:
```git add *.html ```

**Sacar archivos del área de preparación**
Al ser un área de preparación podremos sacar algún archivo de esta área y regresarlo al área local, para eso se hace con el comando:

```git rm --cached _nombre_archivo_ ```

**Las diferentes áreas de Git**

* **Área Local** (Working directory)
Es el directorio de tu computadora. Los archivos en esta área están ***untracked***.
* **Área de Preparación** (Staging area)
Es área de preparación y se colocan los archivos que se confirmarán para ser guardados en el repositorio. Si lo deseamos se pueden regresar al área local. Los archivos en esta área están ***tracked***.
* **Repositorio de Git** (Git Repository)
Es cuando ya se han guardado en la base de datos de git y forman parte de un punto en la historia del proyecto.


**Configurar nombre y correo:**
Antes de poder realizar commits en nuestro repositorio será necesario configurar el nombre y correo, ya que en cada commit Git agrega esta información.

Los comandos para poder consultar y realizar estas configuraciones son:

Para mostrar la ayuda para la opción config
```git config```

Muestra la lista de configuraciones 
```git config --list```

Muestra los directorios en donde se encuentra guardada las diferentes configuraciones (son configuraciones avanzadas): 
```git config --list --show-origin ```

Configurar el nombre
```git config --list --global user.name "_nombre_" ```

Configurar el nombre
```git config --list --global user.email "_email_" ```


**Guardar una versión de nuestros archivos**
Este permite guardar en la base de datos de git una versión en el tiempo de nuestros archivos, es como sacarle una fotografía la cual podemos regresar a ver en cualquier momento en el tiempo, se hace con el siguiente comando:

```git commit -m "_mensaje_" ```

Si se hace solo sin el parámetro -m "_mensaje_", lo que hará git es abrirnos una ventana con el editor configurado para redactar el mensaje de una mejor manera:

```git commit ```

---

### Formas de listar Commits Git:

En cualquier momento podemos consultar la historia de uno de los archivos o de nuestro proyecto de Git, es decir listar de diferentes formas todos los commits realizados durante la historia de nuestro proyecto.

El listado puede mostrar información relevante como sería: la rama en la que nos encontramos, quien los realizo, el hash identificador único de cada commit, fecha y hora, así como el mensaje que identifica cada commit.
Para un archivo específico:

```git log _nombre_archivo ```

Para todo los commits del proyecto:

```git log```

Hay diferentes opciones para mostrar la lista de commits con ```git log``` entre esas variaciones están:

Mostar en una sola línea cada commit:

```git log --oneline```

Mostar estadísticas en cada commit:

```git log --stat```

Muestra donde se encuentra el head point en el log:

```git log --decorate```

Pero si combinamos las siguientes flags tendremos una visualización más precisa de como ha evolucionado nuestro proyecto, es decir podemos visualizar de forma gráfica como se ven las ramas y en qué puntos se han fusionado a la rama principal:

```git log --all --graph --decorate --oneline```

Hay otro comando que muestra absolutamente todos los commit de nuestro proyecto, incluso cuando volvimos atrás en el tiempo con --rest --hard, este comando es:

```git reflog```

**Consultar con más detalle la historia de un archivo**
Mostrará todo los que muestra el comando ```git log``` pero también nos mostrará las versiones que existen de este archivo, así como también mostrara de color rojo lo que se ha eliminado y de color verde lo que se ha agregado. 

```git show _nombre_archivo_ ```

---

### Viajar en el Tiempo en tu proyecto de Git:

En git podemos movernos hacia cualquier punto en el tiempo de nuestro proyecto (commit), esto se puede usando el reset, pero hay 2 tipos: --hard y --soft:
El reset ***--hard*** eliminará todos los commits posteriores al punto en que nos regresamos.
El reset ***--soft*** eliminará todos los commits posteriores al punto en que nos regresamos, pero respeta todo lo que está en el área de preparación.

```git reset _hash_commit_ --rest | --hard```

Otra forma de movernos en el tiempo es utilizando el comando "checkout", con este podemos hacerlo para todos los archivos o solo para un archivo en específico:

```git checkout _hash_commit_ ```


---

### Branchs y Merge:

**Branch (ramas)**
Las ramas permiten trabajar de forma paralela en nuestro proyecto y de esta forma tener más control sobre lo que se agregar al master o rama principal. 

Podemos consultar las ramas (muestra todas las ramas que existen en nuestro proyecto) y es con el siguiente comando:

```git branch ```

Al crear una rama con el siguiente comando solo la crea, pero no nos cambia a la nueva rama, para que lo tengas en cuenta:

```git branch _nombre_rama_ ```

Otra forma de crear una rama y al mismo tiempo cambiarnos a esa nueva rama es con el siguiente comando:

```git checkout -b _nombre_rama_ ```

Para cambiarnos a otra rama en nuestro proyecto usamos:

```git checkout _nombre_rama_a_cambiarnos_ ```

**Merges (fusiones de Ramas)**
Para fucionar ramas (merge) es importante considerar desde donde estamos haciendo el merge, ya que si la hacemos de forma inversa podemos perder cambios importantes, solo considera que la rama en donde estemos parados será la rama que recibiera los cambios de la otra rama, por ejemplo, si tenesmo nuestra rama master y una rama llamada new-feature y queremos añadir esa nueva característica a master, por lo que debemos movernos a master y ahí hacer el merge hacia la rama new-feature. Para hacer un merge usamos el siguiente comando:

```git merge _nombre_rama_a_fucionar_ ```

---

### Repositorios Remotos (GitHub):

Existe repositorios remotos como serían GitHub, GitLab, Atlassian Bitbucket, GitKraken entre otros, el más utilizado y conocido es GitHub.

Para poder subir nuestro código a cualquier repositorio antes mencionado es necesario crear un repositorio remoto en nuestro proyecto con el siguiente comando:

```git remote add origin _url_del_repositorio_remoto_ ```

La ```_url_del_repositorio_remoto_ ``` la obtenemos desde el repositorio que estemos utilizando de cualquiera de las opciones antes mencionadas.

Para consultar los repositorios remotos que tenemos agregados a nuestro proyecto usamos el siguiente comando:

```git remote```

Para obtener más información sobre estos repositorios remotos usamos el comando:

```git remote -v```

**Git Push y Git Pull**
Para subir nuestro proyecto al repositorio remoto que acabamos de crear usamos el comando:

```git push origin main```

Cuando creamos el repositorio y a este le agregamos por ejemplo el README.md o el .gitignore o el archivo de la licencia al el ```git push origin main``` nos mostrara un error, en el cual nos menciona que el repositorio remoto incluye trabajo (otros archivos) que no tenemos en nuestro repositorio local, por lo que nos pide primero integrar los cambios del repositorio remoto lo cual se hacer con el siguientes comando:

```git pull origin main```

Pero nos mostrara una advertencia ya que requerimos de una parámetro para que nos permita fusionar la rama main del repositorio remoto con nuestra rama main de nuestro repositorio local, para eso ejecutamos el siguiente comando:

```git pull origin main --allow-unrelated-histories```

Nos solicitara ingresar un mensaje al commit que crea Git para hacer el merge, ahora debemos ejecutar nuevamente el comendo 

```git pull origin main```

---

### Crear y configurar llave SSH en GitHub:

Primero necesitamos crear una llave SSH en nuestro equipo la cual consta de 2 archivos: ```id_rsa``` y ```id_rsa.pub``` la primera es la llave privada la cual nunca se debe compartir y se quedara siempre en el equipo en el que se configura, y la segunda es la llave publica la cual se puede compartir para poder establecer la comunicación por medio de SSH.

Para crear la llave SSH en nuestro equipo (Windows 10) usamos el siguiente comando:

```ssh-keygen -t rsa -b 4096 -C "_correo_electronico_de_GitHub"```

Al dar Enter preguntara lo siguiente:
1. Solicita la ruta donde se guardará la llave SSH, es recomendable dejar la que nos pone por defecto.
2. Solicita especificar una frase, esta sería como una contraseña que tendríamos que ingresar cada vez que usamos la llave, ya quedará a tu consideración ingresar una o no, si deseas no ingresar esta contraseña solo hacemos Enter. 
*Algo a tener en cuenta es que cuando ingresas la contraseña no visualizaras nada pero si se está capturando.*
3. Solicita repetir la contraseña, si la dejamos en blanco presionamos Enter, pero si ingresaste una contraseña hay que ingresarla exactamente igual.
4. Con esto se crea la llave SSH, la cual es un directorio con 2 archivos: id_rsa y id_rsa.pub
5. Verificamos que el servidor SSH este encendido, se hace con el comando: 
   ```eval $(ssh-agent -s)``` 
   El cual debe mostrar un Pid y un número, esto quiere decir que el servidor SSH está funcionando correctamente.
6. Ahora agregamos la llave, para eso debemos estar en la raíz de nuestro home y se hace con el comando: 
   ```ssh-add ~/.ssh/id_rsa```

Para cambiar la url de un repositorio remoto, esto se podría utilizar cuando tenemos configurado hacer ```git push``` y ```git pull``` con protocolo HTTPS, pero si queremos cambiarlo para hacerlo con SSH, entonces ejecutamos los siguientes comandos:
Primero visualizamos los repositorios remotos:

```git remote -v```

Nos mostrara uno para fetch y otro para push por lo regular se hace para los 2 y se cambia con este comando:

```git remote set-url origin _url_ssh_del_repositorio_remoto_```

---

### Tags y Releases

Los Tag nos sirven para identificar puntos relevantes en la evolución de nuestro proyecto, ya que estos puntos se pueden considerar como un numero de versión especifica.

Para crear un tag se hace de la siguiente forma:
```git tag -a v_numero_version_ -m "_mensaje_del_tag_" _hash_commit_```

Ejemplo de un Tag:

```git tag -a v_0.1 -m "Versión Beta" 5dg23k```

También podemos consultar los Tags que hemos creado con el comando:
```git tag```

Para saber el hash del commit al que hace referencia el Tag es con el comando:
```git show-ref --tags```

También podemos enviar al repositorio remoto (origin) los tags que hemos creado, se hacen de la siguiente forma:
```git push origin --tags```

Para eliminar un tag en Local se hace con el comando:
```git tag -d _nombre_tag_a_eliminar_```

Pero hay un detalle cuando eliminamos un tag en local que anteriormente habíamos subidos al repositorio remoto, este no se elimina del repositorio remoto, este se tiene que eliminar con un comando especial:
```git push origin :refs/tags/_nombre_tag_a_eliminar_```

---

### Lecturas Complementarias

## Git reset VS Git rm
Estos son comando con utilidades diferente:

***Git rm***
Este comando permite eliminar archivos de Git sin eliminar su historial del sistema de versiones, es decir si en un futuro necesitamos recuperar ese archivo solo debemos viajar en el tiempo y recuperarlo con el último commit antes de borrarlo. Este comando no debe usarse así nomás, debe usarse con un flag ya que hay 2 forma de utilizarlo:

Con la flag ```--cached``` Elimina los archivos de nuestro repositorio local y del área de preparación (staging), pero los mantiene en nuestro disco duro, es decir le dice a Git que deje de trackear el historial de cambios de este o estos archivos y pasara al status untracked.

```git rm --cached _nombre_archivo_ ```

Con la flag ```--force``` Elimina los archivos de Git y del disco duro, pero como Git guarda todo hay forma de poderlo recuperar, pero es necesario utilizar comandos avanzados.

```git rm --force _nombre_archivo_ ```

***Git reset***
Este comando nos ayuda a volver en el tiempo (pero no como ```git checkout``` el cual nos permite ir, mirar, pasear y volver), es decir con ```git reset``` volvemos al pasado sin la posibilidad de volver al futuro. Este comando es muy peligroso y debemos usarlo solo en caso de emergencia.

Existe 2 formas de usar ```git reset```: 

Con el argumento ```--soft``` borra todo el historial y los registros de Git pero guardamos los cambios que tengamos en el área de preparación, así podremos aplicar las últimas actualizaciones a un nuevo commit.

```git reset --soft```

Con el argumento ```--hard``` Borra absolutamente todo, absolutamente todo, toda la información de los commits y del área de preparación también borra su historial.

```git reset --hard```

Y también tenemos este comando que nos permite sacra los archivos del área de preparación, NO los borra, si no que los pone en estatus untraked.

```git reset HEAD```



