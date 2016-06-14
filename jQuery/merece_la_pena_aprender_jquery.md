# ¿Adios jQuery?



## Un poco de historia
- Hasta hace unos años había grandes diferencias entre navegadores:
  - Accediendo al DOM
  - Gestionando eventos

- Aparecieron librerías para lidiar con este tipo de cosas:
  - jQuery (2005)
  - Mootols (2007)
  - ....


- ¿Qué ha pasado desde, pongamos el 2010?
  - Microsoft se ha ido acercando a los estándares desde IE9 (2011)
  - El uso de navegadores *no compatibles* ha ido decreciendo.
  - Hay más posibilidades desde JavaScript para acceso al DOM.
  - Frameworks como Angular (desde el 2010) utilizan jqLite, una versión muy reducida de jQuery 


- Frameworks tipo React (2013) empiezan a trabajar con DOM Virtual:
  - Trabajar con el DOM es costoso, mejor trabajar con una versión "más ligera"
  - Si se producen cambios en el DOM Virtual se trasladan al DOM real
  - jQuery trabaja de forma directa con el DOM, así que nos resta eficiencia


## ¿Usamos jQuery?
- Respuesta rápida: NO, salvo por temas de compatibidad
- Respuesta meditada:
  - Si realizas una web (no una webapp) SI
    - Dispones de muchos plugins y desarrollos ya hechos
  - Si realizas una webapp NO, utiliza algún framework
    - En este caso igual haces una webapp y tampoco lo quieres utilizar:
      - ¿SEO? ¿Tiempo de carga? ¿Renderización en servidor? 
      - ¿Componentes que necesitas?



## Selectores en JavaScript
- Nos hemos acostumbrado a usar tanto jQuery que ahora toca volver a aprender:
  - A hacer las cosas con el JavaScript de antes
  - A utilizar nuevas funcionalidades del JavaScript de ahora
- Si es nuestro caso, que venimos de un background con jQuery, [merece la pena echar un ojo a alguna guía](https://toddmotto.com/is-it-time-to-drop-jquery-essentials-to-learning-javascript-from-a-jquery-background/).


### Selector de clase
```
// jQuery
$('.myClass');

// JavaScript
document.getElementsByClassName('myClass');
```


### Selector de id
```
// jQuery
$('#myID');

// JavaScript
document.getElementById('myID');
```


### Selector de etiqueta
```
// jQuery
$('div');

// JavaScript
document.getElementsByTagName('div');
```


### querySelector
```
// Grab the first .myClass class name
document.querySelector('.myClass');

// Return a NodeList of all instances of .myClass
document.querySelectorAll('.myClass');

// Grab the myID id
document.querySelector('#myID');

// Return a NodeList of all 'div' instances
document.querySelectorAll('div');

// Grab the last list Node of .someList unordered list
document.querySelector('ul.someList li:last-child');

// Grab some data-* attribute
document.querySelectorAll('[data-toggle]');
```


## Eventos en JavaScript



### Eventos
```
/*
 * Click
 */
// jQuery
$(elem).on('click', function () {...});

// JavaScript
document.querySelector(elem).onclick = function () {...}
```

### Encolar eventos
```
document.addEventListener('click', function() {
    // ...
}, false);
```

### Evento de Dom Ready
- [Lo soportan la mayoría de navegadores](http://caniuse.com/#search=DOMContentLoaded)
```
document.addEventListener('DOMContentLoaded', function() {
    // DOM ready, run it!
}, false);
```
