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
