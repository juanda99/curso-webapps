# Configuración de Sublime Text



## Editores de código
- Sublime Text, Atom, Brackets
- IDE: **Integrated** Desktop Environment (
    - [WebStorm](https://www.jetbrains.com/webstorm/)
    - NetBeans, Eclipse, Android Studio
    - ¿[Visual Studio Code](https://code.visualstudio.com/)?

- Un IDE tiene muchas cosas "out of the box":
    - Terminal
    - VCS (Version Control System)
    - Task Runner (Grunt, gulp...)
    - Debug, testing...


- Un editor de código tiene:
    - Ventajas:
    	- Más ligero
    	- Lo configuras a tu manera (plugins)
    - Desventajas:
        - Trabajo de configuración
        - No está integrado



## Instalación de Sublime Text 3

- Instalación:

```
sudo add-apt-repository ppa:webupd8team/sublime-text-3 
sudo apt-get update
sudo apt-get install sublime-text-installer
```

- [Instalamos package control](https://packagecontrol.io/installation)
  - Necesario para instalar cualquier plugin posteriormente 
  - Podemos hacer una búsqueda de plugins que nos interesen desde su web
- [Chuleta con los comandos más usados](https://www.cheatography.com/tdeyle/cheat-sheets/sublime-text-3/pdf_bw/)


## Plugins para Sublime Text 

- **AutoFileName**: para autocompletar el nombre de ficheros  
- **HTML Prettify**: Formaterado de js, html y css. Pulsando *CTRL+MAYS+H*
- **Git gutter**: para ver las modificaciones del código respecto al último commit. El resto de interacción con Git mediante consola (aunque existen plugins)
- [**markdown editing**](https://packagecontrol.io/packages/MarkdownEditing): Para editar código en markdown
- **markdown preview**: Para hacer vista previa del markdown


- **Bootstrap 3 Snippets**:  Pulsando **<bs3**
- **jQuery**: snippets para jQuery
- **Emmet**: Ayuda para escribir html y css.


- **nodejs**: para autocompletado
- **ExpressComplete**: para autocompletado de Express

  ```
  rget : router.get("/", function(req,res) { } )
  rpost : router.post("/", function(req,res) { } )
  rput : router.put("/", function(req,res) { } )
  rdel : router.delete("/", function(req,res) { } )
  ```
- **sidebar enhacements**: ofrece más opciones en el menú lateral
    - El menú lateral aparece y desaparece mediante *CTRL + K + B*
    - ¡¡Si no aparecen las nuevas opciones es por haber abierto un fichero con sublime en vez de una carpeta!!


- **[Sublimelinter](http://sublimelinter.readthedocs.io/en/latest/installation.html)**: framework para linters
- **[SublimeLinter-csslint](https://github.com/SublimeLinter/SublimeLinter-csslint)**: linter para CSS
- **SublimeLinter-contrib-eslint**: linter para js según eslint





- **Mocha Snippets**:
  ```
  desc<tab>
  befr<tab>
  aftr<tab>
  suite<tab>
  test<tab>
  ```


- [Añadiremos snippets de React a Sublime](https://github.com/juanda99/react-v0.14-snippets) para poder trabajar con React más rápido

- **Babel** como Syntax Highlighter. Habrá que configurar los ficheros con extensión js para que lo usen por defecto, ver https://packagecontrol.io/packages/Babel


## Snippets para Sublime
- Muchos de los plugins que hemos utilizado incorporan snippets

- Para ver y poder modificar los snippets utilizaremos el paquete **PackageResourceViewer**. [Más info](http://stackoverflow.com/questions/21190392/how-to-change-default-code-snippets-in-sublime-text-3)

- - [Crear y compartir snippets (via GitHub)](http://mandymadethis.com/sharing-sublime-text-snippets/) 


## Configuración tabulaciones
- Necesario para lenguajes como Python
- En nuestro caso por criterio de formato de código
- Fichero Preferences->Settings - Users:

```
{
    "tab_size": 2,
    "translate_tabs_to_spaces": true
}
```