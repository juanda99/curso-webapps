# Sass



## Conceptos generales


### Limitaciones del CSS
- CSS no es un lenguaje de programación:
  - No permite herencia
  - No dispone de variables
  - Las páginas de estilos se pueden volver complejas


### ¿Qué es Sass?
- Sass significa **Syntactically Awesome Stylesheets**
- Es un lenguaje de preprocesado
  - El navegador solo entiende CSS
  - Si utilizamos cualquier otro lenguaje de estilos habrá que compilarlo a CSS


### Ficheros
- La extensión de los ficheros es **.scss** (sassy css) y **.sass**
- Nos centraremos en *.scss* (el más parecido a css)
- Un ficheros *.scss* puede contener también código css


### Como escribir Sass
- Nos centraremos en escribir código css
- Incorporamos técnicas de Sass cuando nos venga bien
- Si utilizamos librerías de terceros:
  - Preferimos código Sass a CSS:
    - Se entiende mejor
    - Es más fácil de modificar



## Sintáxis


### Comentarios 
```
// este comentario no se verá
// cuando compilemos nuestro fichero sass a css
/* pero este otro sí */
```


### Importar ficheros
- En css se evita el uso de @import ya que el código es síncrono y provoca bloqueos
- En sass da igual porque se va a compilar

- Fichero aplication.scss:
```
/* Mi hoja de estilos */
// tendrá el contenido de todo el css de mi aplicación 
// dividido en varios ficheros scss para tener todo organizado
// No hace falta extensión, se sobreentiende scss
@import "buttons";
@import "labels";
...
```
- Al compilar se generará un único fichero **aplication.css**
  - Incluye el fichero *buttons.scss* y *labels.scss*


### Partials
- El compilador también genera los ficheros *buttons.css* y *labels.css*
- Para evitar que se generen se pueden definir como partials:
  - Basta con renombrarlos a _buttons.scss y _labels.scss
  - Solo se compilaran como parte de otro fichero 
- El import no hace falta tocarlo, *@import "buttons* puede importar:
  - *buttons.sass*
  - *button.scss*
  - *buttons.sass*
  - *button.scss*


### Selectores anidados
```
#header {
  height: 72px;
  background: $header-background-color;
  h1 {
    color: white;
    a {
      display: block;
      text-decoration: none;
    }
  }
```
- No se debe abusar del anidado
  - Complica la reusabilidad del código
  - Lo mismo que en css con los selectores descendentes


### Propiedades anidadas
```
.btn {
    text: {
          decoration: underline;
          transform: lowercase;
  }
}
```


### Selector padre: &
```
.btn {
  &.btn-large {
    width: 100px;
    // seleccionamos elementos que tengan class="btn btn-large"
  }
}
```

- Muy útil para pseudoclases:
  ```
  a {
    text-decoration: none;
    &:hover { color: #ccc}
    &:active {color: #ddd}
  }
  ```


### Variables
``` 
$base-color: rgba(blue, 0.5);
$back-color: red !default;

body {
  color: $base-color;
  background-color: #back-color;
}
```
- La fuente en el body será de color azul
- El color de los párrafos será rojo en caso de no haberse definido previamente
- El ámbito de las variables la definen las llaves
    - Si no existen, serán variables globales 


### Otro ejemplo:

```
/*app.scss*/
$rounded: 5px;
@import "buttons"

/*_buttons.scss*/
$rounded: 3px !default;
.btn {
  border-radius: $rounded;
}
```


### Interpolación
- Podemos definir un selector o una propiedad mediante una variable:

```
$elemento = header;
#{$elemento} {
    background-color: red;
}

```


### Mixins
- Bloques de código que se pueden reusar
- Pueden aceptar argumentos
- Si los argumentos tienen valores por defecto, van al final
- Debemos definir el mixin antes de usarlo
- Puede generar código duplicado (no es el caso siguiente debido a los parámetros)
```
@mixin headline($size, $color: red) {
    color: $color;
    font-size: $size;
}
h1 {
    @include headline(12px);
}
article h1 {
    @include headline(12px, blue);
}
```


### Extends
- Similar a mixins pero no acepta parámetros
- Genera menos código duplicado:
  ```
  .icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    @extend .icon;
    /* error specific styles... */
  }

  .info-icon {
    @extend .icon;
    /* info specific styles... */
  }
  ```
  - Genera el siguiente código:
  ```
  .error-icon, .info-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    /* error specific styles... */
  }

  .info-icon {
    /* info specific styles... */
  }
  ```


### Placeholders
- ¿Qué pasa si la clase *.icon* del ejercicio anterior no la usamos en nuestro css?
- ¿Cómo podríamos hacer para codificar nuestro **sass** si el único uso de la clase *.icon* es para ser extendida?
- Utilizaremos placeholders, se codifican anteponiendo un %
  ```
  %icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    @extend %icon;
    /* error specific styles... */
  }

  .info-icon {
    @extend %icon;
    /* info specific styles... */
  }
  ```
- Genera el siguiente código:
  ```
  .error-icon, .info-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    /* error specific styles... */
  }

  .info-icon {
    /* info specific styles... */
  }
  ```


### Mixins vs extends vs placeholders
- El caso anterior se podría hacer con un mixin sin parámetros:
  ```
  @mixin icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    @include icon;
    /* error specific styles... */
  }

  .info-icon {
    @include icon;
    /* info specific styles... */
  }
  ```
- Funcionalmente es lo mismo que usando un placeholder, pero el CSS tiene código repetido:
  ```
  .error-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
    /* error specific styles... */
  }

  .info-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
    /* info specific styles... */
  }
  ```


### Funciones y estructuras de control
- @function
- @if 
  - @else
  - @else if
- @each
- @for
- @while


### Operaciones matemáticas
- Suma, resta, división, multiplicación, módulo
- Funciones definidas:
    - round($number)
    - ceil($number) y floor($number)
    - abs($number)
    - min y max
    - percentage


### Funciones de color
- Evitan usar programas de imágenes para obtener los códigos hexadecimales de los colores

```
.lighten {
  color: lighten($color, 20%)
}
.darken {
    color: darken($color, 20%)
}
```
- Similar con **saturate** y **desaturate** buscando colores más o menos intensos
- Otras funciones:
  - **mix** para mezclar colores
  - **grayscale($color)** para convertir a gris
  - Hay muchas más. 

