# Efectos
Son una forma muy visual para entrar en contacto con dos características muy importantes en jQuery:
- Las funciones de callback
- La concatenación de métodos

## Funciones
Utilizaremos las siguientes funciones:
```
$(selector).hide(speed,callback)
$(selector).show(speed,callback)
$(selector).toggle(speed,callback)
$(selector).slideDown(speed,callback)
$(selector).slideUp(speed,callback)
$(selector).slideToggle(speed,callback)
$(selector).fadeIn(speed,callback)
$(selector).fadeOut(speed,callback)
$(selector).fadeToggle(speed,callback)
$(selector).fadeTo(speed,opacity,callback)
```
*Para ver todas las opciones de efectos recomendamos ver la [http://api.jquery.com/category/effects/ api de efectos de jquery]

### Parámetros de las funciones
- El primer parámetro nos indica la velocidad y puede tener los valores: slow, fast, normal o milisegundos.
- El segundo parámetro es la función que hay que ejecutar en el momento en que se complete la acción de hide o show.
- Los parámetros son opcionales

### Función animate
Con la función animate, podemos hacer efectos más complejos:
- Con valores absolutos o relativos
- Si ponemos varios animates seguidos, los irá encolando (no empezará una instrucción hasta terminar la anterior).

```
$(selector).animate({
      left:'250px',
      opacity:'0.5',
      height:'150px',
      width:'150px'
    });

$("button").click(function(){
  $("div").animate({
    left:'250px',
    height:'+=150px',
    width:'+=150px'
  });
});
```

Pararemos una animación mediante la función stop:
```
$(selector).stop(stopAll,goToEnd);
```

## Funciones de callback
**JavaScript es asíncrono**. Como en otros lenguajes, se ejecutan las instrucciones línea a línea. Sin embargo puede ser que una sentencia no haya terminado su ejecución y ya haya comenzado la siguiente:

```
$("p").hide(1000);
alert("El párrafo se ha escondido ¿AHORA?");
```
En JavaScript las funciones son **(ciudadanos de primer orden)**[http://ryanchristiani.com/functions-as-first-class-citizens-in-javascript/] y se pueden pasar como parámetros. Para evitar el comportamiento asíncrono entre las dos instrucciones anteriores, pasaremos la segunda instrucción como parámetro de la función hide. Para hacer esto tendremos que embeberla en una función:

```
$("p").hide(1000,function(){
  alert("El párrafo se ha escondido AHORA");
});
```
En el ejemplo anterior estamos pasando como parámetro una función anónima, pero podríamos 
haberla definido anteriormente guardándola en una variable:

```
var alerta = function () {
  alert("El párrafo se ha escondido AHORA");
};
$("p").hide(1000, alerta);
```
## Encadenar métodos
Si tenemos que ejecutar varios métodos o acciones sobre el mismo elemento, se pueden encadenar, de modo que el elemento se busque mediante el selector de jQuery una única vez.

```
$("#p1").css("color","red").slideUp(2000).slideDown(2000);
```
También lo podríamos haber hecho así (más legible):
```
$("#p1").css("color","red")
  .slideUp(2000)
  .slideDown(2000);
```

