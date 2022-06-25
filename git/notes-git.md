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

```git add <nombre_archivo> ```

Y también se puede hacer utilizado un punto (.), con esto pasara todos los archivos a los que no se les está dando seguimiento.

```git add . ```

Incluso se puede hacer utilizando los comodines para seleccionar determinados archivos según su extensión, por ejemplo, el siguiente comando solo agregara los archivos con extensión HTML que no se les esté dando seguimiento:
```git add *.html ```

**Sacar archivos del área de preparación**
Al ser un área de preparación podremos sacar algún archivo de esta área y regresarlo al área local, para eso se hace con el comando:

```git rm --cached <nombre_archivo> ```

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
```git config --list --global user.name "<nombre>" ```

Configurar el nombre
```git config --list --global user.email "<email>" ```


**Guardar una versión de nuestros archivos**
Este permite guardar en la base de datos de git una versión en el tiempo de nuestros archivos, es como sacarle una fotografía la cual podemos regresar a ver en cualquier momento en el tiempo, se hace con el siguiente comando:

```git commit -m "<mensaje>" ```

Si se hace solo sin el parámetro -m "_mensaje_", lo que hará git es abrirnos una ventana con el editor configurado para redactar el mensaje de una mejor manera:

```git commit ```

---

### Formas de listar Commits Git:

En cualquier momento podemos consultar la historia de uno de los archivos o de nuestro proyecto de Git, es decir listar de diferentes formas todos los commits realizados durante la historia de nuestro proyecto.

El listado puede mostrar información relevante como sería: la rama en la que nos encontramos, quien los realizo, el hash identificador único de cada commit, fecha y hora, así como el mensaje que identifica cada commit.
Para un archivo específico:

```git log <nombre_archivo> ```

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

```git show <nombre_archivo> ```

---

### Viajar en el Tiempo en tu proyecto de Git:

En git podemos movernos hacia cualquier punto en el tiempo de nuestro proyecto (commit), esto se puede usando el reset, pero hay 2 tipos: --hard y --soft:
El reset ***--hard*** eliminará todos los commits posteriores al punto en que nos regresamos.
El reset ***--soft*** eliminará todos los commits posteriores al punto en que nos regresamos, pero respeta todo lo que está en el área de preparación.

```git reset <hash_commit> --rest | --hard```

Otra forma de movernos en el tiempo es utilizando el comando "checkout", con este podemos hacerlo para todos los archivos o solo para un archivo en específico:

```git checkout <hash_commit> ```


---

### Branchs y Merge:

**Branch (ramas)**
Las ramas permiten trabajar de forma paralela en nuestro proyecto y de esta forma tener más control sobre lo que se agregar al master o rama principal. 

Podemos consultar las ramas (muestra todas las ramas que existen en nuestro proyecto) y es con el siguiente comando:

```git branch ```

Al crear una rama con el siguiente comando solo la crea, pero no nos cambia a la nueva rama, para que lo tengas en cuenta:

```git branch <nombre_rama> ```

Otra forma de crear una rama y al mismo tiempo cambiarnos a esa nueva rama es con el siguiente comando:

```git checkout -b <nombre_rama> ```

Para cambiarnos a otra rama en nuestro proyecto usamos:

```git checkout <nombre_rama_a_cambiarnos> ```

Otra forma de consultar las ramas creadas y su historial es con el los comandos:

```git show-branch ```
```git show-branch --all ```

Existe el un comando que permite visualizar la historia del proyecto de una forma visual con uns software incluido con Git, se abre con el comando:

```gitk ```

**Merges (fusiones de Ramas)**
Para fucionar ramas (merge) es importante considerar desde donde estamos haciendo el merge, ya que si la hacemos de forma inversa podemos perder cambios importantes, solo considera que la rama en donde estemos parados será la rama que recibiera los cambios de la otra rama, por ejemplo, si tenesmo nuestra rama master y una rama llamada new-feature y queremos añadir esa nueva característica a master, por lo que debemos movernos a master y ahí hacer el merge hacia la rama new-feature. Para hacer un merge usamos el siguiente comando:

```git merge <nombre_rama_a_fucionar> ```

En GitHub siempre visualizaremos la rama Main|Master pero si manejamos en nuestro proyecto rmas alternas, que es lo más recomendable hacerlo, es necesario empujarlas al repositorio remoto, pero antes de ejecutar el comando debemos estar en el proyecto local posicionados en la rama que deseamos subir a GitHub y se hace con el siguiente comando:

```git push origin <nombre_rama_a_subir> ```

---

### Repositorios Remotos (GitHub):

Existe repositorios remotos como serían GitHub, GitLab, Atlassian Bitbucket, GitKraken entre otros, el más utilizado y conocido es GitHub.

Para poder subir nuestro código a cualquier repositorio antes mencionado es necesario crear un repositorio remoto en nuestro proyecto con el siguiente comando:

```git remote add origin <url_del_repositorio_remoto> ```

La ```<url_del_repositorio_remoto> ``` la obtenemos desde el repositorio que estemos utilizando de cualquiera de las opciones antes mencionadas.

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

```ssh-keygen -t rsa -b 4096 -C "<correo_electronico_de_GitHub>"```

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

```git remote set-url origin <url_ssh_del_repositorio_remoto>```

---

### Tags y Releases

Los Tag nos sirven para identificar puntos relevantes en la evolución de nuestro proyecto, ya que estos puntos se pueden considerar como un numero de versión especifica.

Para crear un tag se hace de la siguiente forma:
```git tag -a v<numero_version> -m "<mensaje_del_tag>" <hash_commit>```

Ejemplo de un Tag:

```git tag -a v_0.1 -m "Versión Beta" 5dg23k```

También podemos consultar los Tags que hemos creado con el comando:
```git tag```

Para saber el hash del commit al que hace referencia el Tag es con el comando:
```git show-ref --tags```

También podemos enviar al repositorio remoto (origin) los tags que hemos creado, se hacen de la siguiente forma:
```git push origin --tags```

Para eliminar un tag en Local se hace con el comando:
```git tag -d <nombre_tag_a_eliminar>```

Pero hay un detalle cuando eliminamos un tag en local que anteriormente habíamos subidos al repositorio remoto, este no se elimina del repositorio remoto, este se tiene que eliminar con un comando especial:
```git push origin :refs/tags/<nombre_tag_a_eliminar>```

---

### Lecturas Complementarias

## Git reset VS Git rm
Estos son comando con utilidades diferente:

***Git rm***
Este comando permite eliminar archivos de Git sin eliminar su historial del sistema de versiones, es decir si en un futuro necesitamos recuperar ese archivo solo debemos viajar en el tiempo y recuperarlo con el último commit antes de borrarlo. Este comando no debe usarse así nomás, debe usarse con un flag ya que hay 2 forma de utilizarlo:

Con la flag ```--cached``` Elimina los archivos de nuestro repositorio local y del área de preparación (staging), pero los mantiene en nuestro disco duro, es decir le dice a Git que deje de trackear el historial de cambios de este o estos archivos y pasara al status untracked.

```git rm --cached <nombre_archivo> ```

Con la flag ```--force``` Elimina los archivos de Git y del disco duro, pero como Git guarda todo hay forma de poderlo recuperar, pero es necesario utilizar comandos avanzados.

```git rm --force <nombre_archivo> ```

***Git reset***
Este comando nos ayuda a volver en el tiempo (pero no como ```git checkout``` el cual nos permite ir, mirar, pasear y volver), es decir con ```git reset``` volvemos al pasado sin la posibilidad de volver al futuro. Este comando es muy peligroso y debemos usarlo solo en caso de emergencia.

Existe 2 formas de usar ```git reset```: 

Con el argumento ```--soft``` borra todo el historial y los registros de Git pero guardamos los cambios que tengamos en el área de preparación, así podremos aplicar las últimas actualizaciones a un nuevo commit.

```git reset --soft```

Con el argumento ```--hard``` Borra absolutamente todo, absolutamente todo, toda la información de los commits y del área de preparación también borra su historial.

```git reset --hard```

Y también tenemos este comando que nos permite sacra los archivos del área de preparación, NO los borra, si no que los pone en estatus untraked.

```git reset HEAD```



---

### Flujo de trabajo con colaboladores en Git y GitHub

1. La persona que se va unir al proyecto debe ir al repositorio al que se desea unir, ir a la parte "Code" y copiar la url para clonar el repositorio, ya en su equipo se ubica en el directorio que lo va clonar y ejecuta el siguiente comando:

   ```git clone <url_del repositorio_a_clonar>```

   ejemplo:

   ```git clone git@github.com:pepito/thesiteweb.git```

2. Si consultamos este tendra la hsitoria completa dell proyecto y procedemos hacer cambios, modifica un archivo, lo agrega al área de preparación y hace commit, todo bien, al menos hasta ahora. Antes de hacer un ```git push``` recuerda que es buan practica hacer antes un ```git pull```, todo bien no hay cambios y procedemos hacer ```git push``` y ohh sorprise!!! arrija errror y esto se debe a que centinelaX no tenia los permisos en el repositorio para poder modificarlo, donde "pepito" debe agregarlo al proyecto como colaborador.:
```
   ERROR Permission to pepito/thesiteweb.git denied to centinelaX.
   fatal: No se pudo leer del repositorio remoto.

   Por favor asegurese que tiene los permisos de acceso correctos y que el repositorio existe.
```

3. Entonces Pepito en su repositorio del proyecto, vamos a la opción de "Settings" del repositorio (No Settinngs de la cuanta) e ingresamos a la opción **Collborators** y hacemos clic en Add people, buscamos ya sea por su nombre de usuario de Git o por su correo y lo agregamos. Git envia un correo mandando la invitación, una vez que confirme la invitación ya tendra acceso para hacer **push** al repositorio, pero no es buena practica hacerlo al Main|Master del proyecto si no manejarlo por ramas.

4. El dueño del repositrio (Pepito) establecio 2 ramas: header y footer, por lo que Pepito se hará carago del header y CentinelaX se hará cargo del footer, en sus respectivas ramas.

5. Pepito: Empieza a trabajar en el header, añade una imagen para el logo creando un directorio ```./imagenes/dragon2.png``` y nombrando la imagen como dragon2.png y también cambia el color del fondo del body. Agragamos los cambios, hacemos commit a origin main|master y ```git push origin header```, ahora podemos ver como va la rama footer.

6. CentinelaX: Empieza a trabajar, lo primero que debe realizar es ```git pull origin footer``` para traernos los ultimos cambios, incluyendo la rama footer. Ahora si nos ponemos a trabajar en el footer, cuando lo terminemos hacemos commit, despúes sigue subir los cambios al repositorio remoto ```origin/footer```, para eso ejecutamos primero ```git pull origin footer``` (recuerda que siempre antes de hacer un push es necesario hacer un pull) y hacemos el ```git push origin footer```, esto subira en el repositorio los cambios del footer en la rama footer.

7.-Ahora corresponde al encargado del repositorio que en este caso es Pepito hacer los 2 merge a la rama main|master. 
   1. Primero vamos a hacer merge de la rama ```header```, para eso nos movemos a la rama main|master y hacemos el merge con el comando ```git merge header```, nos solicitará el mensaje del commit del merge. Ahora es necesario subir esos cambiso al repositorio remoto, hacemos pull y push.
   2. Hacemos lo mismo para hacer merge de la rama ```footer```, recuerda que debemos estar en la rama main|master y hacemos el merge con el comando ```git merge footer```, nos solicitará el mensaje del commit del merge. Ahora es necesario subir esos cambiso al repositorio remoto, (recuerda hacer antes el git pull) ```git push origin footer```.

8. Lista ya tenemos en la rama master fusionado el header y el footer, lo recomendable una vez que se unifica una rama es eliminarla pero ya es a tu criterio hacerlo.


---

### Flujo de trabajo con personas que son colaborandores mediante Pull request

Puedes colaborar en un repositorio de Git y GitHub aun cuando no eres colaborador (y también siendolo), se hace realizando un ```pull request```, el flojo es el sguiente:

1. Suponiendo que tenemos los mismo reposditorios, el de Pepito y CentinelaX, si detectamos un bug en un archivo del proyecto, para hacer la corección será necesario crea una rama la cual denominaremos fix-branch, la cual debe estar actualiza con main|master y procedemos a corregir los bugs.

2. Lo siguiente será empujar la rama fix-branch a GitHub haciendo ```git push origin fix-branch``` 

3. Ahora será necesario agregarlos al área de preparación y confirmar los cambios haciendo commit y volvemos hacer ```git push origin fix-branch```

4. En GitHub en la página principal del proyecto de la cuanta del responsable (Pepito) seleccionamos la rama fix-branch y no arrojara un mensaje que hay diferencia con respecto la rama main|master.

5. Para unirlo GitHub sugiere  hacer un ```pull request``` o también da la opción de hacer un ```Compare & pull request```, lo primero que que nos solicita GitHub es especificar que ramas va comprar, sería de la rama main|master contra l arama fix-branch.

6. Al hacer un pull request GITHUB permite agregar detalles, es decir especificar por que se estan solicitando esos cambios y que quede documentado.

7. En la parte derecha se pueden especificar más detalles, como: solicitar a alguien más que los revise (Reviews), Labels para clasificarlo, así comoProjects y Milestones y hacemos clic en el boton ```Create pull request``` así todos los del equipo tendran concocimiento de lo que se corrigio.

8. Ahora CentinelaX abre el repsositorio y verá que hay un pull request, ademas que si se asigno a alguien del equipo le llegara un correo que se le asigno como reviews y podra visualizar a detalle todo sobr eel pull reques, que cambios y que rama quiere unir.

9. Si consulta en la pestaña ```Files changed``` puede visualizar que porcion de codigo cambiaron, ahí en la parte derecha se localiz ael botón ```Review changes```, si hacemos clic aqui podemos especificar si lo aceptamos o en su defecto no lo aceptamos porque requerimos más cambios. Tiene las opciones: Comment (realzar algun comentario de feelback), Approve (especificas que son factibles los cambios) y Request changes (solicitamos más cambios), en todos los caso debemos jsutificarlo en el mensaje. Todo esto se va agregando en el historial del pull request y quedara documentado.

10. El propietario (Pepito) recibira una alerta en su repositorio (y notificación vía correo electrónico) donde le solicitan hacer más cambios en el pull request, por lo que  se procede a realizar las modificaciones solicitadas.

11. Para empezar hacer cambios primero hacer un ```git pull origin fix-branch``` solo para actualizar nustro repositorio local, y procedemos a realizra los cambios, una vez realizados los cambios hacemos el commit respectivo con los cambios y volvemos a empujar todo en el repositorio en la rama fix-branch ```git push origin fix-branch```.

12. Ahora nos vamos a GitHub al pull request y hacemos clic en la pestaña ```Files changed```, podmeos visualizar los cambios, ahora procedemos a enviarle un mensaje donde se le avisa que los cambios solicitados ya se han realizado y le podemos solicitar a CentinelaX que haga el merge, hacemos clic en el boton Comment.

13. CentinelaX recibira la notificación sobre lo que se agrego al pull request donde se le solicta hacer el merge, revisa los cambios, podmeos hacer clic en el botón ```Review changes```, seleccionamos la opción Approve y le mandamos un mensaje, ya se esta aprobando realizar el pull request. Hay que considerar que los cambios esten aprobados no seignifica que ya se hizo el merge.

14. Ahora será responsabilidada del encargado de proyecto definir quien es el que realizara el merge (y en egneral todos los merges). Si hay colaboradores estos tienen la faccultad de poder realizar los merge, pero si es una persona que no es colaborador del proyecto esta no podrá hacerlo, ya que solo lo podrán hacer el dueño del repositorio y los colaboradores del proyecto.

15. Para hacer la fusión hacemos clin en el boton ```Merge pull request```, en la ventana que nos abre ya podemos ahora si hacer clic en el botón ```Confirm merge``` y esto realizara el merge (realiza el commit correspondiente dle merge) y también cierra el pull request.

16. Una vez cerrado el pull request, podemos eliminar la rama fix-branch y GitHub nos da la opornidad de eliminarla, por lo que procedmos a eliminarala, si nos movemos en el repositorio a la rama priencipal main|master deberan estar lso cambios realizadas por medio del pull request.

17. Ahora en el repositorio local de Pepito aun existe la rama fix-branch, primero ejecutamos un ```git pull origin fix-branch``` pero no se va poder, porque ye hemos eliminado la rama fix-branch del repositorio remoto, pero como ya se hizo merge con main|master hacemos el ```git pull origin main|master``` y esto nos va actualizar la rama principal, ahora mi repositorio local esta actualizado a la última versión.

---

### Flujo de trabajo con personas que no son colaborandores

Para explicar este flujo vamos a quitar de colaborador a CentinelaX, por lo que al ya no ser colaboradora del proyecto ya no puede hacer merge, podria clonar el repositorio pero no podrá hacer push de ningun tipo al proyecto de Pepito, ya no tendra permisos de push, lo único que podra realizar es clonar el proyecto y hacer una mejora pero lo tendra que hacer mediante un pull request pero con algunas variantes.

1. Para poder colaborar en el repositorio estando en el GitHub de CentinelaX buscamos el repositorio en el que queremos colaborar, podemos darle en ```Watch``` para que el dueño del repositorio tenga conocimiento que estoy observando los cambios en el mismo. Tambien podmeos darle una estrella en ```Start```.

2.- Pero lo más importante que podemos hacer es hacer un ```Fork```, esto no straera  anuestro repositorio una copia del estado actual del proyecto y clonarlo, solo se les puede hacer Fork a repositorios publicos. Empezara a clonar el repositorio en nuestro GitHub.

3. Una vez hecho el Fork lo primero que necesitamos hacer es traerlo a nuestro equipo, seleccionamos el directorio donde lo vamos a guardar y procedemos a clonarlo, por lo que copiamos de GitHub la url haciendo clic en ```Code``` y en la terminal ejecutamos lo siguiente: ```git clone _url_proyecto_a_clonar ```, esto nos va clonar el proyecto en local, con todo el historial del proyecto, es decir que si hacemos un git log mostrara todos los commites realizados durante el mismo.

4. El siguente paso es hacer alguna mejora al proyecto que pueda convencer al dueño del repositorio de aceptar mis cambios, se modifican los archivos necesarios, despues hacemos su o sus respectivos commits, si hacemos un ```git status``` me dirá que estamos más adelante qu ela rama main|master por los commits que se hayan realizado.

5. Lo que sigue es subir nuestros cambios al repositorio que hicmos fork (no al repositorio del proyecto) con el comando ```git push``` y con esto ya tendremos el repositorio actualizado.

6. El siguiente paso es crear un ```pull request``` para ver si el dueños del repositorio le agradan nuestas mejoras y lo une a su main|master de su proyecto.

7. En el GitHub de CentinelaX vamos a creamos el pull request haciendo clic en pull requests y despés en el botón ```Create pull request```, GitHub me pregunta que ramas deceamos comparar y hacer merge, por de defecto nos muesta que sería de nuestra rama main|master a la rama main|master del proyecto de Pepito, y más abajo nos muestra cuales son los cambios.

8. Una vez que verificamos que todo esta correcto hacemos clic en el boton ```Create pull request```, nos solicitará ingresar un mensaje donde expicamos la mejora que queremos contribuir y hacemos clic en el botón ```Create pull request```, esto ya creará lo creara y notificará al dueño del proyecto así como a los colaboradores.

9. Como podemos observar en GitHub no tenesmos nosotros de hacer el merge del pull request ya que este solo lo puede ahcer el dueño o algun colaborador, lo que si se puede hacer es cerrar el pull request o volver a comentar.

10. Ahora en el GitHub de Pepito (dueño del respositorio) entramos al proyecto y ahi parcerá el pull request, podemos visualizar que cambios sugiere, su mensaje de justificación para analisar si son factible sus mejoras.

11. Ingresamos a ```Files changes``` y ahi podmeos hecer clic en ```Review changes``` agregamos un mensaje y seleccionamos alguna opción: se Commets | Approve | Request changes, y hacemos clic en Submit review, para est caso mandamos mensaje de OK y aprobamos los cambios (Approve) y hacemos el merge, si revisamos, los cambios de CentinelaX deberan estar unidos a mi main|master.

12. Si Pepito sigue trabajando y haciendo cambios antes de hacer nosotos cualquier cambio (algun commit) debes traernos los ultimos cambios con ```git pull origin main```, en el caso que tuvieramos cambios pendientes de hacer commit en el area de preparación será necesario hacerles commit para no perder los cambios, y una vez que nos traemos los cmabios ahora hacemos un ```git push origin main``` para tener actualizado nuestro repositorio con los últimos cambios.

13. Ahora hay un detalle el cual consiste en que el repositorio origial de Pepito ya tuvo cambios y el repositorio que se le hizo fork esta desfazado por eso cambios, para actualizarlo tenemos que hacer los siguiente: en el GitHub de CentinelaX en donde nos muestra la alerta (en la qu emenciona que estamos n commits atras) hacemos clic en el boton ```Fetch upstream``` seleccionamos la opción ```Compare``` nos mostrará los detalles de los cambios, como sería los commits así como los cambios se puede hacer de 2 formas: la más sencilla es que en GitHub seleccionemos la opción ```Fetch upstream``` o hacerlo desde la consola.

14. Para actualizar nuestro repositorio remoto desde la consola sería como primer paso crear otra fuente para hacer pull, si cosultamos los repositorio remotro con ```git remote -v``` nos mostrará que solo tenemos ```origin```, para eso tenemos que ir al proyecto original y copiar la url de su proyecto y en la cosola vamos a ejecutar el comando ```git remote add upstream _url_repositorio_original_``` esto nos creará el repositorio remoto original, si volvemos a consultar los repositorios remotos ahora tendremos 2: origin y upstream.

15. Ahora será necesario hacer un ```git pull upstream main``` para traernos todos los cambios del repositorio original a nuestra rama main|master y con esto ya nos traemos los cambios, si hacemos un git status podemos ver los commits agregados. El siguiente paso será hacer un ```git push origin main|master``` y listo ya esta actualizado!!!


---

### Ignorar archivos en Git - **.gitignore**

Git permite ignorar archivos, es decir Git no les dará seguimiento, esto es util cuando tenemos archivos con información sencible como claves de acceso a servicios como serían bases de datos o llaves de acceso a otros sitios, también con archivos como la carpeta de node_modules entre otros.

Será necesario crear un archivo en la raíz del proyecto llamado ```.gitignore``` en el cual se van a especificar los nombre de los archivos o directorios que deseamos excluir del seguimiento de Git.

Se pueden especificar grupos de archivos usando los comodines como el asterisco (*), por ejemplo si deseamos excluir todos los archivos con extensión jpg seria ```*.jpg```, para especificar nombre de archivos  seria: ```misCredenciles.js``` y ´para directorios sería ```node_modules/```.


---

### Archivo README.md

Es un archivo que describe tu repositorio de Git en el sitio GitHub, donde el .md significa formato Mark Down, es un formato que permite darle un poco de formato permitiendo utilizar titulos de varios tamaños, negritas, cursivas, enlaces, fragmentos de codigo, imaágenes, etc.

Solo teines que crear un archivo en la raíz del proyecto llamado ```README.md``` y listo, ya pudes empezar a explicar aspectos de tu proyecto, que es, para que sirve, documentación, etc.


---

### GitHub Pages

GitHub tiene un servicio de hosting gratis para páginas estaticas y este disponible en internet.

TODO


---

### Git Rebase

Git Rebese es una opción que tenemos en Git para reorganizar el trabajo realizado, es decir, esta opción nos permite integrar uno o una seríe de commits en un punto especifico de proyecto, se la rama master o cualquier otra rama, pero todo esto se haría sin hacer un merge.

El uso de Git Rebase es recomendable usarla d emanera local, nunca en repositorios remotos ya que se considera una mala practica.

El escenario en el que se realiza un Git Rebase e spor ejemplo cuando detectamos que hay un detalle en la rama principal, pero deseamos solucionarlo sin hacer un Merge, es decir integrar "n" commits a la rama main|master pero si que quede historial como sería con un merge.

La implementación sería crear una rama (que llamaremos fix-bug), se hacen lso cambios requeridos con sus respectivos commits, para integrarlos y estando en la rama fix-bug hacemos ```git rebase main|master``` esto integrar los commit d ela rama fix-bug a la rama main|master, ahora nos cambiamos a la rama main|master y hacemos un rebase pero ahora hacia la rama fix-bug ```git rebase fix-bug```, con esto quedarán integrados los commits en la rama fix-bug y si eliminamos esta rama en el hsitorial esta rama nunca existio. Para liminar una rama es ```git branch -D _nombre_rama_a_eliminar_```.


---

### Git Stash

Git Stach nos permite guadar cambios de forma temporal, es decir si nosotros ya agregamos archivos al area de perparación, pero no estamos listos para hacer un commit y no queremos perder estos cambios por que nos necesitamos cambiar de rama para eso usamos ```git stash```, esto nos guardara los cambios que teniamos en el area de preparación.

Para consultar los stash que tenemos se usa el comando: ```git stash list``` y nos mostrara la siguiente información:
```stash@{0}: WIP on main: _hash_corto_ _mensaje_commit_```, donde en la primera parte nos muestra el consecutivo del stash, despues hace referencia en que commit se realizo y también muestra el mensaje del commit.

Cuando ya queremos ahora si retomar con lo que teniamos el stash nos movemos a la rama en la que se realizo el stash y ejecutamos ```git stash pop``` con esto recuperamos los cambios que teniamos en ele area de preparaicón y ya podemos hacerle commit o descartarlos.

Tamnbién podemos agregar un stach a una rama, para eso cuando ya tengamos guadado el stash ejecutamos ```git stach branch _nombre_rama_``` esto nos cambiara a la rama que especificamos y con los cambios que teniamos en el stash, ya aqui podmeos ya sea omitir los ambios o en su defecto hacerle commit.

Cuando creamos un estash y decidimos no utilizarlo lo podemos eliminar con el siguiente comando: ```git stash drop```.


---

### Git Clean

Git permite eliminar archivos inecesarios, archivos que creamos por error o por algunas prubas que estemos realizando, como Git sabe cuales son los arhcivo a los que se les esta dando seguimiento, los demas archivos los considera basura.

Para cosnulatar que archivos puede ser limpiados usamos el siguiente ocmando ```git clean dry-run``` el cual mostrar una lista de archivos que tal vez deseamos eliminar.

Para eliminarlos d enuestro proyecto ejecutamos el comando ```git clean -f```, esto los eliminara d enuestro proyecto, considera que ya no será posible recuperarlos.

Algo a considerar es que si por error duplicamos un directorio con un archivo que esta trakeado (Git le esta dando seguimiento) como el nombre del archivo es igual (solo el nombre del directorio cambia) al que tenemos en la carpeta original de la cual lo copiamos, git clean no lo eliminará y tendremos que eliminarlo a mano. Otro escenario en el que git no limpiara los archivos es por que estan siendo ignarados por el archivo .gitignore.


---

### Git Cherry-pick

Este comando permite agregar a una rama un commit cualquiera de otra rama, solo necesitamos conocer el hash del commit que quermos agregar y estar posicionado en la rama a la que deseamos que se agregue ese commit, s ehace con el comando: ```git cherry-pick _hash_a_unir_ ``` y este commit se añadira a nuestra rama, solo hay que tener mucho cuidado con este comando ya que modifica la historia, usarlo solo en caso de emergencias.


---

### Git amend

Este comando permite enmendar el último commit, si por ejemplo teniamos que modificar 2 archivos: el html y el css, despue svamos modificamos el html y hacemos el commit, pero necesitabamos que los cambios del archivo css quedaran en ese último commit, lo que podmeos hacer despues de haber realizado el commit (el cual contiene los cambios pero solo del html) es hacer los cambio necesarios en el archivo css, despues lo agregamos al área de preparación ```git add _nombre_archivo_```, una ves que ya lo agregamos ejecutamos el siguiente comando ```git commit --amend```, esto nos abrira el editor de texto con la información del último commit, por lo que en este último commit vamos a incluir también el archivo CSS, también vamos a poder cambiar el mensaje y así todo quedará en el mismo commit. 

Esto solo es funcional para el último commit.


---

### Git Reflog

Con este comando podemos consultar la historia completa dle proyecto, incluso mostrar información que no podemos obtener con Git log, pero es muy últil si por alguna razón hicimos git reset --hard hacia un puntpo del proyecto, todo lo que habia despues ya no se podra acceder desde ese punto con git log pero si con git reflog, así este comando es solo en caso de emergencia y hay que usarlo con mucho cuidado.


---

### Git Grep 

Este comando nos permite buscar determinadas palabras en nuestro proyecto, cuantas veces usamos la palabra "color" por ejemplo y nos mostrara el archivo y toda su linea: ```git grep _palabra_a_buscar_```

Si deseamos saber en que nuemor de línea se muestra agregamos el  al ejecutar el comando ```git grep -n _palabra_a_buscar_```

Podemos obtener el número de veces que se muestra una pálabra se hace con el flag -n y no sdira cuantas veces aparece la palabra en cada archivo que la encontro ```git grep -c _palabra_a_buscar_```

También podemos buscar palabras en los mensajes de los commits, esto se hace con el comando: ```git log -S _palabra_a_buscar_```


---

### Git shortlog

Este comando permite saber información de los integrantes que han cotribuido al proyecto, como por ejemplo cuanto commits,

Muestra el numero de commits y los mensajes de cada integrante del equipo:
```git shortlog```

Muestra solo el nombre de las personas que han hecho commits
```git shortlog -sn```

Muestra absolutamente todos los commits (incluso los borrados)
```git shortlog -sn --all```

Muestra absolutamente todos los commits (incluso los borrados) pero quitando los de los merge
```git shortlog -sn --all --no-merges```


---

### Alias en Git

Los alias permite asignar un nombre corto a comandos demaciado largos, para gregar nuestros alias:

Agregamos un alias para el comando git stat
```git config --global alias.stats "shortlog -sn --all --no-merges"```

Podemos crear el alias arbol con el git log y todas sus flags
```git config --global alias.arbol "log --all --graph --decorate --oneline"```

### Git blame

Este comando pemrite mostrar line por linea quien lo ha realizado, se hace con el comando:
```git blame _nombre_archivo_```

Para saber quien modifico que en un archivo:
```git blame _nombre_archivo_ -L35,53```

Para saber quien modifico que en un archivo mejor identado:
```git blame _nombre_archivo_ -L35,53 -c```


---

### Para consultar la documentación web de cualquier comando

Se ahce con el comando:
```git _comando_ --help```


---

### Para consultar mas a detalle las ramas

Consultar las ramas:
```git branch```

Consultar las ramas remotas:
```git branch -r```

Consultar todas las ramas locales y remotas, también muestra la rama en la que estamos parados con un asterisco:
```git branch -a```


