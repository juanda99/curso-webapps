# Sass



## Conceptos generales


### ¿Por qué Sass?
- CSS no es un lenguaje de programación:
  - No permite herencia
  - No dispone de variables
  - Las páginas de estilos se pueden volver complejas

- Sass significa **Syntactically Awesome Stylesheets**
- Es un lenguaje de preprocesado
  - El navegador solo entiende CSS
  - Es necesario compilarlo a CSS


### Ficheros
- La extensión de los ficheros es .scss (sassy css) y .sass
- Nos centraremos en el primero de ellos (el más parecido a css)
- Un ficheros .scss puede contener código css (es válido)


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
  - Incluye el fichero buttons.scss y labels.scss


### Partials
- El compilador también genera los ficheros buttons.css y labels.css
- Para evitar que se generen se pueden definir como partials:
  - Basta con renombrarlos a _buttons.scss y _labels.scss
  - Solo se compilaran como parte de otro fichero 
- El import no hace falta tocarlo, ```@import "buttons``` puede importar:
  - buttons.sass
  - button.scss
  - buttons.sass
  - button.scss


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


### & para el selector padre
```
.btn {
  &.btn-large {
    width: 100px;
    // seleccionamos elementos que tengan class="btn btn-large"
  }
}
```
- Muy útil para pseudoclases:
a {
  text-decoration: none;
  &:hover { color: #ccc}
  &:active {color: #ddd}
}


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
- Sass también traduce el valor de rgba al propio de CSS *rgba(0, 0, 255, 0.5)*


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
- Podemos definir un selectores o propiedades mediante una variable:

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
- 
```
@mixin headline($size, $color: red) {
    color: $color;
    font-size: $size;
}
h1 {
    @include headline(12px);
}
h1 {
    @include headline(12px, blue);
}
```


### Mixins vs extends vs placeholders

- - Se deben evitar el uso de extends
- http://krasimirtsonev.com/blog/article/SASS-mixins-extends-and-placeholders-differences-use-cases
- 
### Placeholders

- - Mediante %
- Se parecen a los partials:
    - Se pueden extender 
    - No pueden ser selectores por si solos

**Mixins**: propiedades parecidas (valores por parámetro) y usadas varias veces
**Extends**: Conjunto de propiedades iguales y usadas varias veces (el css que generan es peor, ver link). Ejemplo plantillas de wordpress
**Funciones**: Operaciones comunes para determinar valores

### Funciones y estructuras de control
@function
@if y @else y @else if
@each
@for
@while


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

