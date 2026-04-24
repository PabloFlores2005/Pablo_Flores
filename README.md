# Trabajo Individual

Pablo Gabriel Flores Guarachi

## Clase 1

### Historia de Git

El linus se enojó un día y decidió crear Git.

### Instalar y settear Git

Entras a la página y según tu SO, instalas el paquete.

Una vez instalado, verificas que esté disponible usando git --version.

Luego, setteamos el user y email usando git config --global user.name/email "valor".

### Archivos de Git

Cada repo tiene 2 archivos:

* README.md que explica el proyecto, con sus formatos.
* .gitignore que indica qué no se debe subir al repo.

### Markdown

Se abre con cualquier repo, usas Markdown para los .md.

* Usa numerales (#) para títulos.
* Guiones (-) para líneas.
* Semi comillas(```) para escribir código.
* Para imágenes ![texto](url)

### Comandos de Git

* Para iniciar un repo local, git init. Crea un archivo .git, el cual tiene toda la información del repo.
* Con git status, muestras tus archivos, los que han sido modificados.
* Git add para añadir tus archivos.
* Git commit -m "mensaje" para crear un commit. Al hacer git status, confirmas que los cambios han sido guardados.
* Git logs para ver los logs del repo, como un historial.

## Clase 2

### States

Git ve los estados, son los siguiente.

#### Directorio de trabajo

Git aún no guarda, lo tiene detectado. Revisa tu directorio.

Los archivos los cataloga en untracked (sin seguimiento, no tiene versión previa, nuevo) y modified (archivo modificado, eliminado o con un nombre nuevo).

Aquí, el archivo gitignore es importante porque indica qué archivos no pasan al repo, los que no quieres subir. Solo añades los archivos y directorios.

Para descartar el cambio, usas git restore, pero cuidado, borras todo el cambio. Puedes recuperar un archivo borrado con git restore.

#### Stage Area

Preparado, le dices a Git qué guardar. Antes, los preparas. Usas git add [file] para guardar un archivo, git add . para guardar todos. Para sacar el archivo del stage area, usas git restore --staged [file]. De untracked a guardado. De guardado a modified.

#### Local Repo

Con los cambios confirmados, se gfuardan en el repo. El historial ya tiene cambios. Para hacerlo, usas git commit -m "mensaje", el cual crea un punto de guardado de todos los archivos en staged.

Para ver todos los commits, usas git log. Para ver más simple, git log --oneline, resume el ID.

Para deshacer el último commit, usa git reset --soft HEAD~1, dice vuelve al último punto de guardado. Se borra el commit, y vuelven los archivos al stage area.

Para cambiar el nombre del commit, git commit --amend -m "nuevo mensaje". Cambia el ID.

#### Repo Remoto

Se suben los cambios.

### Buenas Prácticas

El mensaje del commit debe ser descriptivo.

1. Que los commits sean atómicos, no por cada pequeño cambio ni tampoco por cada gran volumen. Deben ser cambios pequeños pero que tengan una relación. Solo con incluir una coma o "y" ya describes dos acciones diferentes. Commit por cada cambio mínimo, iteraciones pequeñas.
2. Los commits deben ser descriptivos, con verbos imperativos (acciones, add, change, fix, remove). Nunca usar puntos, comas tal vez, pero puntos no. Son innecesarios. Usa como máximo 50 caracteres en los mensajes de commit, simple y directo. Y usa un prefijo para hacerlos más semánticos, "tipo": "descripción". Ahora, los más comunes son feat (nueva feature), fix (bugs), perf (mejorar performance), build (para el sistema de build), ci (pipeline), docs (documentación), refactor (refactorizas el código), style (cambios UI) y test. Si el commit es más complicado, añade un contexto, no hay nombre del commit. Para eso, ejecutas git commit, así sin nada, abre su editor, en la primera línea añades el commit normal, y de bajo, el cuerpo con la descripción.

## Clase 3

### Github

Es una plataforma en la nube para alojar y gestionar proyectos. Git es el control de versiones, Github es el servidor.

#### Crear cuenta

Ve a github.com, seleccionas sign up para registrarte. Dentro, rellenas tus datos o inicias con cuenta de Google o Apple. El username es importante, no se puede cambiar. No lo hagas con la cuenta institucional porque les quitan cuando terminen la carrera, lo debes vincular a otras cuentas. Para verificar la cuenta, se hace un puzzle/captcha.

#### Crear repo

Luego, se crea un repositorio, dando el nombre, una descripción, la visibilidad (público, privado), add README, add .gitignore y add license (licencias del código).

Si creas un repo con tu nombre de usuario, se lo puede usar como portafolio.

#### Configurar SSH

HTTPS para clonar no hay problemas, pero para el trabajo en equipo es molesto porque siempre pide credenciales. Lo mejor es SSH.

En windows, abres Git bash. Ejecutas ssh-keygen -t ed25519 -C "Email" para generar una llave.
Git es el que gestiona commits y repos, Github es el servicio para trabajar en equipo. Copias el contenido y luego, vas a settings, SSH keys, le ponen título y pegas la llave. Para comprobar que funciona, ssh -T <git@github.com>, debe responder con un Hi para comprobar que está autenticado.

Si clonaste con HTTPS, se puede usar este comando para cambiar el puntero de github y que ya no pida autenticación: git remote set-url origin "<git@github.com>:User/Repo.git"

#### Configurar repo

Si tienes un repo existente, git remode add origin repo, para que el local se conecte con el remoto. Para renombrar ramas, git branch -M nuevo_nombre. Para subir cambios, git push -u origin main (u por ser la 1ra vez).

Un commit puede ser de máximo 100MB. El repo tiene un límite de hasta 10GB. Para subir cambios, git push. No soporta validación de password, por eso es mejor SSH. Git push origin rama, para indicar al servidor y rama. Para bajar cambios, git pull origin rama. O git pull.

## Clase 4

### Git remote

Permite gestionar conexiones con los repositorios remotos. git remote -v para ver las URLs donde apunta el repo, git remote add apodo "URL" para vincular con uno nuevo, git remote set-url apodo "URL" para cambiar hacia dónde apunta.

### Configurar múltiple SSH

Entras a la carpeta .ssh para ver las llaves que generas. Creas un archivo config; dentro, se puede definir host de la siguiente forma:

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
```

El archivo se lee de arriba hacia abajo, los Host deben ser de nombres distintos. Para varios SSH, cambias el identity file. El host es el alias de la conexión.

Para comprobar conexión, ssh -T git@host

### Configuraciones locales

Puedes ver configuraciones en git config list. Lo anterior no va a usar otro user de git porque usamos global. Para usar otro usuario, usamos configuraciones locales.

Hay una jerarquía:

1. Sistema
2. Global: Lo que haces con git config --global. En la config list, aparecen arriba.
3. Local: Se imponen a todo, ejecutando git config y ya. En la config list, aparecen abajo.

### Git checkout

Permite movernos entre ramas, pero también puedes apuntar a otro commit. Para eso, git checkout con el Hash. Para volver al commit actual, git checkout main. Pero si vuelves a main, alerta que el HEAD está desacoplado, que para guardar el cambio, se debe crear una nueva rama.

Para recuperarlo, git checkout con el hash. Y para guardarlo, git checkout -b "branch". Creas una nueva rama.

### Recomendaciones

1. No trabajes mucho en Detached HEAD.
2. Limpiar el directorio de trabajo.
3. Aprende, es bueno.
