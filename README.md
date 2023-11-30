# curso de git

quiero acomodar esto para poder entender mejor como funciona y bueno, si quieren crear ramas, todo es bienvenido.

## instalar git
para instalar git en linux (que lo mas probable es que ya lo tengas) utiliza esto:
<pre>
-- arch
sudo pacman -S git
-- ubuntu/debian
sudo apt install git
-- fedora
sudo dnf install git
</pre>

una vez tengamos instalado git, crearemos una carpeta donde se contenera nuestro repo.
ya una vez creado, entraremos y pondremos las configuraciones para el git:
<pre>
-- usuario para el repo.
git config --global user.name "tunombre"
-- tu correo para el repo.
git config --global user.email tucorreo@gmail.com
-- para configurar el editor que abrira git.
git config --global core.editor "tu editor de codigo"
-- para ver los cambios en la configuracion.
git config --global -e
</pre>

ahora, una vez que tenemos la configuracion, vamos a iniciar el repositorio:
<pre>
-- si quieres que la rama principal se llame main, en vez de master, pone esto (aviso!! si iniciaste el repo, borra la carpeta ".git" y inicialo nuevamente):
git config --global init.defaultBranch main
-- para iniciar el repo.
git init
</pre>

## estado del repositorio: gracias a esto, vamos a poder ver el seguimiento de los archivos a ingresar
<pre>
git status
</pre>
 ## una vez que crees el archivo que quieres ingresar en el git (va en la carpeta que creamos) y lo hayas modificado y guardado, git se dara cuenta y si pones "git status" dara esto:
<pre>
-- marcara la rama que te encuentras.
En la rama master
-- si ingresaste cambios al repositorio.
No hay commits todavía
-- para hacer un primer guardado en el git.
Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que será confirmado)
	tuarchivo
no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)
</pre>
## sabiendo que esta sin seguimiento, (git aun no lo tiene como archivo de repo) vamos a ingresarlo a stage (cambios a ser confirmados)
<pre>
git add tuarchivo
</pre>
### si hacemos un "git status" nos dara esto:
<pre>
En la rama master
No hay commits todavía
Cambios a ser confirmados:
  (usa "git rm --cached <archivo>..." para sacar del área de stage)
    nuevos archivos: tuarchivo
</pre>
### para sacarlo del stage, usamos "git rm --cached tuarchivo" esto, te dara la opcion de verificar los cambios que haras en el archivo del repositorio
## en stage, solo pasan los cambios que hicimos

## bueno, si hemos hecho todos los cambios, y queremos guardarlo, un paso antes de subirlo a commits(parte final de la subida de archivos) quedara como archivo a ser confirmado:
### si colocamos nuevamente "git status" saldra esto:
<pre>
Cambios a ser confirmados:
  (usa "git rm --cached <archivo>..." para sacar del área de stage)
	nuevos archivos: tuarchivo
</pre>

## si estamos seguros que queremos meter el archivo, lo enviamos a commits. con esto, vamos a poner un comentario para los cambios que hemos creado en los archivos.
<pre>
git commit -m "comentario para el archivo modificado"
</pre>

# ya con eso, estamos diciendo, cuales son los archivos, creados o modificados, que iran al repositorio (tanto a github, gitlab, etc).

# eliminacion de un archivo:
para eliminar un archivo, podemos directamente escribir esto:
<pre>
git rm tuarchivo
-- para ya guardar los cambios, para el servidor usamos:
git commit -m "tuarchivo fue eliminado"
</pre>

# se puede restablecer, si lo eliminamos por error (solo si no se hace el commit, luego de eliminarlo)
<pre>
git restore --stage tuarchivo
</pre>
### con eso, lo restableceremos, pero, como esta en el stage, se puede restablecer. si hacemos un commit, creo que ya no se puede

# renombrar archivos:
para renombrar un archivo, podemos utilizar esto:
<pre>
git add tuarchivo nombre_de_cambio
</pre>

si damos un "git status" dara esto.
<pre>
En la rama master
Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
	renombrados:     prueba2.txt -> prueba.txt
</pre>

### para hacer los cambios, metemos un commit y, logico, el comentario.
<pre>
git commit -m "renombré tuarchivo"
</pre>

# para evitar que un archivo o directorio no se meta al repo. creamos en el directorio principal. crearemos un archivo, llamado ".env" que contendra, cosas para mi. por ejemplo:
<pre>
password = 1234
user = Dubranachoo
-- para directorios es:

</pre>

### luego, crearemos otro archivo llamado ".gitignore" donde agregaremos los archivos, rutas a ignorar.
<pre>
.env
directorio_a_omitir/
</pre>

#### si hacemos un status, tendremos esto:
<pre>
En la rama master
Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que será confirmado)
    .env
	.gitignore

no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)
</pre>

# le hacemos un add .gitignore
### y lo commiteamos, agregando un comentario de "git ignore o algo asi"
<pre>
git add .gitignore
git commit -m "archivo gitignore"
</pre>

# cada vez que modifiquemos un archivo, vamos a tener que hacer un add, para agregarlo a stage, y un commit para meterlo al repo y comentar las modificaciones.
### si queremos saber que modificamos en el archivo, usamos "cat y el nombre del archivo"
<pre>
cat tuarchivo
</pre>

saldra lo que tenga el archivo.

# Log del repo:
esto es importante para saber que hicimos y que modificamos.
### con "git log --oneline" veremos el log del repo en una sola linea

# crear ramas.
las ramas sirven para modificar archivos, de manera tal que no influyan directamente en el main, es muy bueno si no queres sobreescribir los archivos directamente.
## para ver las ramas usaremos:
<pre>
git branch
</pre>
### para crear una rama usaremos:
<pre>
git checkout -b ramab
</pre>

ahora si hacemos un "git branch", nos dara las ramas y en cual estamos parados (con un *).
<pre>
  main
* ramab
</pre>

## para cambiar de rama solo usamos "git checkout nombre_de_la_rama".

## para poner los cambios de una rama, en la rama principal.
### estando en la rama "main", vamos a tipear lo siguiente:
<pre>
git merge nombre_de_la_rama
</pre>

con eso, vamos a hacer que, los cambios que hallamos hecho en la rama, migren hacia la rama main agregando los cambios y manteniendo lo demas.

# Metiendo el repo en github
para meter el repo en github, (y los cambios realizados, o el nuevo repositorio), debemos crear el repositorio en la pagina primero. (crearlo sin agregar el README, lo agregas luego)
luego, github te dará unos comandos, solo los cuales vamos a usar 2, que son estos:
<pre>
git remote add origin url_de_tu_repo
git push -u origin main
</pre>

bueno, con el remote, le decimos git, donde guardaremos nuestro repositorio
con el push, enviaremos el repositorio al main (por eso cambiamos el nombre de la rama anteriormente).

## cuando hagas el push, te pedira username y password. username, usa el de git.
### password la sacas de:
#### "perfil -> settings -> developer settings -> personal access tokens -> generate new token"
cuando llegues ahi, pone que te haga un token clasico "classic" y le marcas las casillas
### write
porque sino, no te deja subirlo.
#### con el token generado, lo copias, y lo pegas como contraseña. despues de haber puesto el username.
##### le das enter y listo, has subido tu repositorio a github.

