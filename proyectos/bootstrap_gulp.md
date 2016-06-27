# Web con bootstrap y gulp


## Instalación

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


## Servidor web
- Para empezar a trabajar modificando código, lo mejor es levantar un servidor web:

  ``` 
  gulp serve
  ```
- Nos ofrece cambios en vivo (live reload).


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

## Crear mi propio theme
- Para empezar no me harán falta todos los import de css de bootstrap, así que me creo una copia *_bootstrap.scss* en mi carpeta de styles, que será el que utilice. Lo llamaré *_theme.less* (ya que al modificar Bootstrap voy a generar mi propio tema)

- El main.scss de mi carpeta de estilos quedará así:

```
$icon-font-path: '../fonts/';

// bower:scss
@import "_theme.scss";
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

- Para cambiar el estilo de boostrap, lo mejor, en la medida de lo posible es utilizar sus variables:
  - Es el modo que han definido los creadores para hacer las modificaciones de forma sencilla.
  - Observa que también podrías hacer las modificaciones vía web, pero sería más costoso:
    - No siempre tienes claros los cambios
    - [Hay páginas que te dejan ver los cambios en vivo](http://bootstrap-live-customizer.com/) mejorando la página "Customize" del propio bootstrap.


### Ejemplo de uso

- Vamos a buscar una interfaz sin botones redondeados:
  - Miramos el fichero *_buttons.scss* que define los botones.
  - Vemos que hay un mixin que es el encargado del estilo redondeado:

  ```
   @include button-size($padding-base-vertical, $padding-base-horizontal, $font-size-base, $line-height-base, $btn-border-radius-base);
  ```
  
- Comprobamos que efectivamente es el encargado, viendo el css que hay definido en el mixin button-size:

```
// Button sizes
@mixin button-size($padding-vertical, $padding-horizontal, $font-size, $line-height, $border-radius) {
  padding: $padding-vertical $padding-horizontal;
  font-size: $font-size;
  line-height: $line-height;
  border-radius: $border-radius;
}
```

- En el fichero de variables de Bootstrap vemos como la definen:
```
$btn-border-radius-base:         $border-radius-base !default;
```

- Añado en mi fichero *_theme.scss* la variable que quiero utilizar, en mi caso $border-radius-base, ya que quiero que los input tampoco tengan los bordes redondeados:

  ```
  //defino mis variables, las podría llevar a un fichero separado, si fueran muchas...
  //no pasa nada porque se definan de nuevo posteriormente, ya que llevan el modificador default!
  $border-radius-base: 0px;

  // Core variables and mixins
  @import "bower_components/bootstrap-sass/assets/stylesheets/bootstrap/variables";
  @import "bower_components/bootstrap-sass/assets/stylesheets/bootstrap/mixins";
  ....
  ```
  
  ## Añadir plugins
  
  - Vamos a buscar un plugin para hacer una validación más específica:
    - Le podremos dar el css que nosotros quereamos, sin ser algo específico del navegador
    - Tendrá métodos adicionales para la validación (además de los que podamos definir nosotros).

```
bower search validation
bower install jquery.validation --save
```

- Lo "enganchamos" a nuestro sitio web mediante el comando:

```
gulp wiredep
```
  
- En nuestro fichero main.js añadimos el código necesario para cargar nuestro plugin con nuestro formulario (al formulario le he añadido el id *frmcontactar*):

```
$('#frmcontactar').validate();
```

- Comprobamos el funcionamiento mediante *gulp serve*
- Si ya está terminado el proyecto podemos generar nuestro código final mediante *gulp build*
