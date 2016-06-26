# Web con bootstrap y gulp

- Se trata de seguir trabajando el ejercicio de la práctica anterior pero con un entorno de desarrollo más potente.

- De los [generadores para Yeoman](http://yeoman.io/generators/), utilizaré [webapp](https://github.com/yeoman/generator-webapp#readme)

- Instalo las dependencias:
```
npm i -g yo gulp-cli bower
npm i -g generator-webapp
```

- Creo mi aplicación
```
mkdir proyecto
cd proyecto
yo webapp
```
Seleccionaremos Sass, Bootstrap y Modernizr. No haremos test, así que da igual BDD que TDD.

- Eliminamos el body del fichero app/index.html con cuidado de no borrar las llamadas a las hojas de estilos y js, **ni los comentarios previos ni posteriores**

- Podemos dejar el fichero app/styles/main.scss simplemente así:

```
$icon-font-path: '../fonts/';

// bower:scss
@import "bower_components/bootstrap-sass/assets/stylesheets/_bootstrap.scss";
// endbower
```


## Página de contactar

- Añadimos un menú responsive en la parte de arriba de la página

```
bs3-navbar-responsive + tab
```

- Como lo queremos fijo arriba, añadiremos la clase *navbar-fixed-top*
- Como lo queremos centrado, cambiaremos la case container-fluid por container
- El código final queda así:
 
```
  <nav class="navbar navbar-inverse navbar-fixed-top" role="navigation">
    <div class="container">
      <!-- Brand and toggle get grouped for better mobile display -->
      <div class="navbar-header">
        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-ex1-collapse">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand" href="#">Mi web de cervezas</a>
      </div>
  
      <!-- Collect the nav links, forms, and other content for toggling -->
      <div class="collapse navbar-collapse navbar-ex1-collapse">
        <ul class="nav navbar-nav navbar-right">
          <li class="active"><a href="#">Inicio</a></li>
          <li><a href="#">Mis cervezas</a></li>
          <li><a href="#">Contactar</a></li>
        </ul>


      </div><!-- /.navbar-collapse -->
    </div>
  </nav>
```

- He añadido un formulario al body, los comandos que he utilizado son los siguientes:
```
bs3-input:text:h + tab
bs3-input:email:h + tab
bs3-input:submit:h + tab
```

- Para que quede bien añadimos un container para el body (*container* o *container-fluid*) que englobe al formulario (MAYS + CTRL + g en *emmet*, y escribimos .container).
- También añadimos un padding al body:
```
body {
  padding-top: 70px;
}
```

## Modificar variables
- Para empezar no me harán falta todos los import de css de bootstrap, así que me creo un *_bootstrap.scss* en mi carpeta de styles, que será el que utilice.

- El main.scss de mi carpeta de estilos quedará así:

```
$icon-font-path: '../fonts/';

// bower:scss
@import "_bootstrap.scss";
// endbower

body {
  padding-top: 70px;
}
```

- Mi nuevo fichero *_bootstrap.scss* tendrá estas rutas en sus import:
```
// Core variables and mixins
@import "bower_components/bootstrap-sass/assets/stylesheets/bootstrap/variables";
@import "bower_components/bootstrap-sass/assets/stylesheets/bootstrap/mixins";
...
```
