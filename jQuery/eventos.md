# Eventos



## Como funcionan los eventos en jQuery
```
$(".mienlace").click(function(mievento){
   mievento.preventDefault();
   alert("Has hecho clic. Como he hecho preventDefault, no te llevaré al href");
});
```
- El evento se define sobre todos los objetos seleccionados mediante el selector jQuery
  - En este caso todos los elementos con *class="mienlace"*
- El tipo de evento lo definimos mediante la función click u otra similar.
- El evento recibe como parámetro una función que será la manejadora del evento.


- La función manejadora del evento tiene a su vez un parámetro *mievento* que nos permite utilizar las propiedades o métodos del evento en cuestión.
  - En este caso utilizaremos el método *preventDefault()*  



## Listado de Eventos


### Eventos relacionados con el ratón
- **click()** 
  - Sirve para generar un evento cuando se produce un clic en un elemento de la página.

- **dblclick()** 
  - Para generar un evento cuando se produce un doble clic sobre un elemento. 
  - Se generarán también dos eventos click()


- **mousedown()** 
  - Para generar un evento cuando el usuario hace clic independientemente de si lo suelta o no. 
  - Sirve tanto para el botón derecho como el izquierdo del ratón. 
  - Útil para drag&drop
```
$("#p").mousedown(function (b) {
    alert(b.which);
    //b puede ser 1, 2 o 3 (botón izquierdo, central o derecho)
});
```


- **mouseup()** 
  - Para generar un evento cuando el usuario ha hecho clic y luego suelta un botón del ratón. 
  - El evento mouseup se produce sólo en el momento de soltar el botón.
- **mousemove()** 
  - Evento que se produce al mover el ratón sobre un elemento de la página.
```
$("#contendedor").mousemove(function (c) {
        $(this).html("El ratón se está moviendo. Las coordenadas son " + c.pageX + ", " + c.pageY);
    });
```


- **mouseover()** y **mouseout()**
  - Sirve para lo mismo que los eventos mouseover y mouseout de Javascript. Se produce cuando el ratón está sobre un elemento, pero tiene como particularidad que pueden producirse varias veces mientras se mueve el ratón sobre el elemento, sin necesidad de haber salido (por los elementos anidados).


- **mouseenter()** y **mouseleave()**
  - Normalmente preferiremos estos eventos respecto a los originales de javascript ya que se ejecutarán sólo una vez.


- **hover()** 
  - Esta función en realidad sirve para manejar dos eventos, cuando el ratón entra y sale de encima de un elemento. Por tanto espera recibir dos funciones en vez de una que se envía a la mayoría de los eventos.
  - A menudo utilizaremos este evento mejor en vez de mouseenter() y mouseleave().
  ```
  .hover(function() {
       Put in mouse enter function here
    }, function() {
       Put in mouse leave function here
  });
  //Ejemplo:
  $("#p").hover(function () {
       $(this).css("background-color", "blue");
    }, function () {
       $(this).css("background-color", "white");
  });
  ```


- **toggle()** 
  - Sirve para indicar dos o más funciones para ejecutar cuando el usuario realiza clics, con la particularidad que esas funciones se van alternando a medida que el usuario hace clics.
```
$("#p").toggle(function () {
  $(this).css("background-color", "blue");
  }, function () {
     $(this).css("background-color", "red");
  }, function () {
     $(this).css("background-color", "yellow");
});
```


## Eventos relacionados con el teclado


- Primero se ejecuta uno o varios eventos keydown(), en función de si se mantiene o no la tecla pulsada. Luego uno o varios eventos keypress() y luego un único evento keyup().


- **keydown()** 
  - Se produce en el momento que se presiona una tecla del teclado, independientemente de si se libera la presión o se mantiene.
  - Funciona con todas las teclas.


- **keyup()** 
  - Se ejecuta en el momento de liberar una tecla.
  - Funciona con todas las teclas.
- **keypress()** 
  - Se ejecuta como respuesta a una pulsación e inmediata liberación de la tecla.
  - No se dispara con las teclas ALT, MAYS, CTRL.


- Los navegadores almacenan de forma diferente las teclas pulsadas. La propiedad which del evento nos permitirá trabajar sin preocuparnos de ello.
- Ejemplo:

  ```
  <html>
    <head>
      <script type="text/javascript" src="jquery-1.8.2.min.js"></script>
      <script type="text/javascript">
        $(document).ready(function () {
      $("#keypress").keyup(function (key) {
        alert(key.which);
      });
        });
      </script>
    </head>
    <body>
      <p>Key Up Test: <input type="text" name="keypress" id="keypress" /></p>
    </body>
  </html>
  ```



## Asociación de DOM y eventos


### Métodos bind(), live() y delegate() 
- En la versión de jQuery 1.7 han intentado unificar las APIs de manejo de eventos en los métodos on() y off(). 
- Estos métodos sustituyen a los antiguos bind(), delegate() y live().


### Método on()

```
$(elements).on(events [, selector] [, data], handler);
```

- Las funciones para eventos vistas hasta ahora, como click, son atajos a la función on():

```
// Asignar un manejador de eventos usando click
$("#header a").click(function() {
    // manejar el evento
});

// Asignar un manejador de eventos usando on
$("#header a").on("click", function() {
    // manejar el evento
});
```

- Estas dos construcciones son equivalentes, pero on() permite hacer muchas más cosas...


- Permite usar un mismo manejador de eventos para múltiples elementos html suscribiendo el manejador a un elemento padre. Dado el siguiente código html:

```
<div id="content">
    <a href="#">enlace1</a>
    <a href="#">enlace2</a>
    <a href="#">enlace2</a>
</div>
```

Si queremos asignar el mismo manejador de eventos a todos los enlaces, podemos hacerlo de la siguiente forma:

```
$("#content").on("click", "a", function() {
    // manejar el evento
    // $(this) apunta al <a> que ha generado el evento
});
```


- Ventajas:

  - Sólo se crea una única función, independientemente del número de enlaces que tengamos, reduciendo el consumo de recursos.
  - Es válido para elementos que no existen todavía. Si apareciese un nuevo elemento *a* dentro del *div*, automáticamente estaríamos manejando su evento click. Esto es especialmente útil cuando generamos html dinámicamente.


- Permite definir un mismo manejador de eventos para distintos tipos de eventos

```
$("p").on("click mouseenter mouseleave", function(e){
  if ($(this).css("color")!="rgb(250, 100, 0)")
    $(this).css("color", "rgb(250, 100, 0)");
  else
    $(this).css("color", "rgb(150, 0, 255)");
  })
```


### Método off()

- Para esta acción, contábamos con varios métodos como unbind(), die() o undelegate(). 
- De nuevo, el objetivo principal de la nueva instrucción es reemplazarlos a todos de un modo consistente.
- La sintaxis de off() resulta similar a la de on():<br/>
  ```
  $(elements).off( [ events ] [, selector] [, handler] );
  ```
- Con off(), todos los parámetros son opcionales. Cuando se utiliza en su forma más simple, *$(elements).off()*, se eliminan todos los eventos asociados al conjunto seleccionado.


### Ejemplo
- El evento click se asocia o se elimina del elemento #theone.
- Uso de find para optimizar el código
- Uso de click() para mayor legibilidad

```
<!DOCTYPE html>
<html>
 <head>
  <style>
     button { margin:5px; }
     button#theone { color:red; background:yellow; }
  </style>
  <script src="http://code.jquery.com/jquery-latest.js"></script>
 </head>
 <body>
   <button id="theone">Does nothing...</button>
   <button id="bind">Add Click</button>
   <button id="unbind">Remove Click</button>
   <div style="display:none;">Click!</div>
   <script>
      function aClick() {
         $("div").show().fadeOut("slow");
      }
      $("#bind").click(function () {
         $("body").on("click", "#theone", aClick)
         .find("#theone").text("Can Click!");
      });
      $("#unbind").click(function () {
         $("body").off("click", "#theone", aClick)
         .find("#theone").text("Does nothing...");
      });
   </script>
 </body>
</html>
```



