# Configuración de Sublime Text

## Editores de código
- Sublime Text, Atom, Brackets...
- IDE: **Integrated** Desktop Environment (
    - [WebStorm](https://www.jetbrains.com/webstorm/), 60€ aprox.
    - [Visual Studio Code](https://code.visualstudio.com/), en beta
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

- [Instalación y configuración de Sublime Text 3 en Ubuntu 14.04 para desarrollo Web](http://www.formandome.es/linux/instalacion-y-configuracion-de-sublime-text-3-en-ubuntu-14-04-para-desarrollo-web/)

```
sudo add-apt-repository ppa:webupd8team/sublime-text-3 
sudo apt-get update
sudo apt-get install sublime-text-installer
```

- [Instalamos package control](https://packagecontrol.io/installation)

- Por ejemplo ahora un [plugin para edición de MarkDown](https://packagecontrol.io/packages/MarkdownEditing)
    - Podemos cambiar el esquema de colores desde los settings de usuario
    - Utilizamos [GFM](https://help.github.com/enterprise/11.10.340/user/articles/github-flavored-markdown/)

## Plugins para Sublime Text 
- Utilizaremos los siguientes plugins para desarrollo web:
- **nodejs**: para autocompletado
- **ExpressComplete**: para autocompletado de Express, por ej:

```
rget : router.get("/", function(req,res) { } )
rpost : router.post("/", function(req,res) { } )
rput : router.put("/", function(req,res) { } )
rdel : router.delete("/", function(req,res) { } )
```

- **sidebar enhacements**: ofrece más opciones en el menú lateral
    - El menú lateral aparece y desaparece mediante CTRL + K + B
    - Si no aparecen estas opciones es por haber abierto un fichero con sublime en vez de una carpeta
- **Sublimelinter** y **SublimeLinter-contrib-eslint**
- **Emmet**: Escribimos más rápido html y css
- **HTML Prettify**: Formaterado de js, html y css. Pulsando *CTRL+MAYS+H*
- **Mocha Snippets**:
```
desc<tab>
befr<tab>
aftr<tab>
suite<tab>
test<tab>
```
- **Git gutter**: para ver las modificaciones del código respecto al último commit. El resto de interacción con Git mediante consola (aunque existen plugins)
- **markdown editing**
- **Snippets para react**:
    - Utilizamos  **React ES6 Snippets** ya que está basado en el paquete de Facebook pero con características de JavaScript ES6 y ES7
    - Tendremos que modificar los snippets que utilicemos para cumplir con nuestro estilo de código. Para ver y poder modificar los snippets utilizaremos el paquete **PackageResourceViewer**. Más info en http://stackoverflow.com/questions/21190392/how-to-change-default-code-snippets-in-sublime-text-3.
    - **Babel** como Syntax Highlighter. Habrá que configurar los ficheros con extensión js para que lo usen por defecto, ver https://packagecontrol.io/packages/Babel
    
    - Compartir snippets: http://mandymadethis.com/sharing-sublime-text-snippets/

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

