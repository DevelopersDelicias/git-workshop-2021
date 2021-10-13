# Taller de Control de Versiones con Git

## Introducción

### Conceptos básicos

- Control de versiones: Forma en la que llevamos un registro de las diferentes versiones de un documento, archivo o cualquier otro elemento que sea suceptible a cambiar en el tiempo, así como de la información relacionada a sus cambios.

- VCS: Version Control System. Así se conoce a las diferentes aplicaciones para lograr el control de versiones. Se clasifican en Centralizados y Distribuidos.

- Repositorio: Conjunto de archivos que compone un proyecto, así como aquella meta-información que registra las diferentes acciones dentro del mismo.

### ¿Qué es Git?

Git es una herramienta muy útil para el desarrollo de Software que nos permite llevar el control y administración de los cambios que se van produciendo en el código fuente de un proyecto.

### ¿Cómo se instala?

1. Descargar de la página oficial de Git https://git-scm.com/downloads
2. Seguir los pasos del asistente y finalizar.

### Práctica 1: Crear un repositorio de Git

1. Abrir la consola de GitBash
2. Crear una carpeta donde se alojarán nuestros proyectos

```
$ mkdir  path/to/your/projects/
```

3. Creamos una nueva carpeta que contendrá nuestro proyecto (repositorio)

```
$ cd  path/to/your/projects/
$ mkdir taller-git-2021
$ cd taller-git-2021
```

4. Inicializamos un nuevo repositorio

```
$ git init
```

5. Exploramos el contenido de la carpeta creada

```
$ ls -la

-rw-r--r-- 1 cisne 197609 130 oct. 12 16:35 config
-rw-r--r-- 1 cisne 197609  73 oct. 12 16:35 description
-rw-r--r-- 1 cisne 197609  23 oct. 12 16:35 HEAD
drwxr-xr-x 1 cisne 197609   0 oct. 12 16:35 hooks/
drwxr-xr-x 1 cisne 197609   0 oct. 12 16:35 info/
drwxr-xr-x 1 cisne 197609   0 oct. 12 16:35 objects/
drwxr-xr-x 1 cisne 197609   0 oct. 12 16:35 refs/
```

### Configuraciones iniciales en Git

En Git podemos tener 2 niveles de configuración:

- Por proyecto
- De manera global

Para ver la lista de configuraciones actuales de nuestro proyecto ejecutamos el siguiente comando:

```
$ git config --list
```

Para ver las configuraciones globales:

```
$ git config --list --global
```

Para ver el valor actual de una configuración basta con ejecutar lo siguiente:

```
$ git config <<llave_config>>
```

Ejemplo:

```
$ git config user.name
```

Para establecer un nuevo valor se hace de la siguiente manera:

```
$ git config <<llave_config>> <<nuevo_valor>>
```

Ejemplo:

```
$ git config user.name "John Doe"
```

### Práctica 2: Configurar nuestro nombre de usuario y correo en el repositorio actual

1. Lista las configuraciones actuales del proyecto
2. Verifica los valores actuales para el nombre de usuario y password actuales (`user.name` y `user.email`)
3. Configura los valores correspondientes a tu Nombre completo y correo que utilices habitualmente.
4. Verifica que los cambios se han realizado correctamente.

### Comandos básicos

#### `git status`

Este comando nos permite ver el estado actual de los archivos que forman parte de nuestro repositorio

Los estados más comunes son:

- **Untracked**: En este estado los archivos aún no han sido registrados por Git, por lo que es requerido agregarlos al Area de preparación (Stage Area)

- **Added (new)**: Son archivos nuevos que han sido agregados al Área de preparación.

- **Modified (not staged)**: Son archivos que han sufrido un cambio pero aun no se han agregado al Stage Area

- **Modified (staged)**: Son archivos que ya se encuentran listos para confirmar los cambios.

- **Commited (confirmados)**: Son archivos que ya se encuentran registrados por Git, y se guarda un punto de guardado de la versión actual.

> Nota: Tambien ocurre lo mismo cuando borramos un archivo previamente confirmado.

#### `git add`

Nos permite agregar un archivo nuevo, modificado o eliminado al Stage area.

Para agregar un archivo(s) especifico(s) podemos hacerlo así:

```
$ git add mi_archivo otro_archivo micarpeta/archivo
```

Tambien podemos agregar una expresión para agregar más de un archivo

```
$ git add *.txt
$ git add nuevo_*
$ git add carpeta/*/*.java
```

Si queremos agregar todos los archivos

```
$ git add -A
```

O si queremos todos los archivos a partir de la carpeta actual

```
$ git add .
```

> Tambien es posible agregar parcialmente algun cambio de un archivo con el parametro `-p`

#### `git commit`

Una vez que tenemos 1 o más archivo en el Área de preparación, podemos indicarle a Git que nos cree un commit o un punto de salvación.

```
$ git commit
```

Cada commit requiere un mensaje para poder agregar una descripción de los cambios que hemos efectuado. En este caso nos abrirá el editor que tengamos definido en la configuración y podremos ingresarlo.

Si no deseamos abrir el editor, podemos pasarlo en el mismo comando con el parámetro `-m`

```
$ git commit -m "Descripcion de los cambios efectuados"
```

#### `git log`

Con este comando podremos visualizar los diferentes commits que tiene nuestro repositorio ordenados del último hacia atras.

```
$ git log
commit 8eb62385f3f65b60004a2e8bad5f7e2991731ef0 (HEAD -> master)
Author: Benjamin Cisneros <cisnerosbarraza@gmail.com>
Date:   Tue Oct 12 22:15:00 2021 -0600

    Archivo modificado

commit 0a6511ba6ae41e6fae81ea09e6cb455b921e3b19
Author: Benjamin Cisneros <cisnerosbarraza@gmail.com>
Date:   Tue Oct 12 21:57:26 2021 -0600

    Nuevo archivo
```

Cada commit contiene un numero hexadecimal que lo identifica y es generado automáticamente por Git.
Este valor es coocido como _Hash_ o código _SHA-1_.

Se puede usar los primeros digitos del Hash para ciertas operaciones siempre y cuando no exista otro commit que empiece con los mismos digitos.

#### `git show`

Con este comando podremos ver los cambios especificos de un commit.

```
$ git show
commit 8eb62385f3f65b60004a2e8bad5f7e2991731ef0 (HEAD -> master)
Author: Benjamin Cisneros <cisnerosbarraza@gmail.com>
Date:   Tue Oct 12 22:15:00 2021 -0600

    Archivo modificado

diff --git a/hello.txt b/hello.txt
index e69de29..a19abfe 100644
--- a/hello.txt
+++ b/hello.txt
@@ -0,0 +1 @@
+Hola
```

Tambien podemos usarlo de la siguiente manera:

```
$ git show CODIGO_HASH
```

#### `git diff`

Este comando nos permite ver las diferencias entre el archivo versionado y las modificaciones actuales.

```
$ git diff
diff --git a/hello.txt b/hello.txt
index a19abfe..b85602e 100644
--- a/hello.txt
+++ b/hello.txt
@@ -1 +1,4 @@
-Hola
+Hola Fulanito
+
+Esta es una nueva línea
+
```

> Nota: Sólo nos muestra los archivos modificados que no han sido agregados al Stage Area, pero no los archivos nuevos.

Si deseamos ver los archivos agregados al Stage Area usamos el siguiente comando

```
$ git diff --cached
```

#### `git help`

Nos permite obtener información relevante de cualquier comando de Git

```
$ git help COMANDO
```

Ejemplo

```
$ git help commit
```

Nos abrirá nuestro navegador por defecto con una página html que contiene más detalles sobre el comando en cuestión.

### Práctica 3: Agregar los primeros cambios a nuestro repositorio y revisar el historial de cambios.

1. Abrimos en nuestro editor de preferencia la carpeta que contiene nuestro repositorio.
2. Creamos un archivo de texto básico y le ponemos como nombre `README.md`.
3. Ingresamos un pequeño texto como el siguiente:

```
# Mi Proyecto

Aquí una descripción de lo que hace mi proyecto.

```

4. En la consola checamos el estado del repositorio con `git status`

5. Agregamos el archivo con `git add README.md`

6. Revisamos de nuevo el estado

7. Hacemos un commit del primer archivo

```
git commit -m "Version inicial de README.md"
```

8. Hacemos algún cambio en nuestro archivo README

```
# MyFacebook

Básicamente es una copia de Facebook pero más humilde :).

```

9. Revisamos el estado del repositorio

10. Checamos los cambios en el archivo con `git diff`

11. Realizamos un nuevo commit

```
git commit -m "Modificación a README.md" -a
```

12. Repetimos los pasos 8-11 para agregar otros cambios.
13. Revisamos el historial de commits con `git log`
14. Revisamos cuales fueron los cambios del segundo commit con `git show HASH_SEGUNDO_COMMIT`
15. Consultamos la ayuda del comando `log` con `git help log`

### Ignorar archivos

Existen ocasiones que ciertos archivos son generados automaticamente por otras herramientas, tales como logs, archivos compilados, archivos temporales, etc.., los cuales no deben ser incluidos dentro del control de cambios.

Para evitar que esos archivos sean incluidos dentro del control de versiones por error, se recomienda contar con un archivo `.gitignore` donde se enlisten los archivos.

Ejemplo:

```
$ cat .gitignore

archivo_ignorado.txt
*.log
build/
```

Existe un sitio muy util que nos permite obtener una lista de patrones comunes de archivos a ignorar dependiendo del tipo de proyecto en el que estemos trabajando.

https://www.toptal.com/developers/gitignore

Introducimos las palabras clave como por ejemplo Java, Ruby, PHP, etc.. y una vez que tengamos la lista le damos clic en Create.

Nos va a generar un archivo el cual podemos copiar y pegar en nuestro archivo `.gitignore`.

## Trabajando con branches localmente

### ¿Que es un branch?

En términos simples es espacio aislado de trabajo en el que podemos hacer cambios independientes del flujo principal, para poder despues integrarlos a este.

### Listar los branches

Para listar los branches solamente ejecutamos el siguiente comando:

```
$ git branch
  dev
* master
  otro-branch
```

> Nota: El branch con `*` es el branch actual

### Crear un branch

Para crear un nuevo branch usamos el siguiente comando:

```
$ git branch nombre_del_branch
```

Ejemplos

```
$ git branch mibranch
$ git branch ticket-156
$ git branch features/feature-ABC
```

### Movernos entre diferentes branches

Para movernos a otro branch usamos el comando checkout

```
$ git checkout nombre_del_branch
```

Ejemplo

```
$ git checkout mibranch
```

Tambien es posible crear el branch y movernos en un solo paso con el siguiente comando.

```
$ git checkout -b nombre_del_branch
```

### Merge de un branch a otro

Una vez que hemos realizado los cambios en nuestro branch podemos integrarlos a otra rama con los siguientes pasos:

1. Movernos a la rama que deseamos integrar los cambios
2. Ejecutamos el comando `git merge branch_a_integrar`

### Eliminar un branch

Una vez que hemos integrado el branch o ya no es necesario podemos eliminarlo de la siguiente manera.

```
$ git branch -d branch_a_eliminar
```

Si hemos realizado algún commit y aun no se ha integrado, Git nos advierte que no puede eliminarlo aun, pero podemos forzar su eliminación con el siguiente comando:

```
$ git branch -D branch_a_eliminar
```

### Renombrar un branch

Si deseamos cambiar el nombre del branch ejecutamos el siguiente comando:

```
$ git branch -m nombre_actual nuevo_nombre
```

## Git como herramienta de trabajo colaborativa

### Crear una cuenta en Github

Vamos al sitio https://github.com/ y creamos una nueva cuenta contando con un correo, nombre de usuario y password.

### Crear un repositorio remoto

Dentro de Github localizamos el boton de New y le damos clic.

Luego le damos un nombre a nuestro branch, seleccionamos si es de acceso Publico o Privado y le damos en crear.

### Ligar repositorio local con remoto

git remote add origin git@github.com:DevelopersDelicias/taller-git-2021.git
git branch -M main
git push -u origin main

### Subir cambios locales al repositorio remoto

git push

#### SSH config

```
ssh-keygen -t rsa
```

Nos solicita algunos datos, como la ubicacion del certificado, passphrase, entre otros. Podemos darle los valores por defecto.

Una vez terminado nos creara un archivo `~/.ssh/id_rsa.pub` el cual tendremos que copiar y pegar dentro de nuestra cuenta de Github.

https://github.com/settings/keys

### Actualizar repositorio con cambios remotos

git pull

### Clonar un repositorio existente

git clone git@github.com:DevelopersDelicias/taller-git-2021.git
