
# jQuery



## ¿Qué es jQuery?

jQuery es una librería de funciones JavaScript: *Write less, do more* 

Su funcionalidad principal es la siguiente:
- Selección y manipulación de elementos HTML y CSS
- Funciones de eventos en HTML
- Efectos y animaciones de JavaScript
- Ejecución de peticiones asíncronas (AJAX)
- Ofrecer compatibilidad en la programación en JavaScript con distintos navegadores.


## Versiones de jQuery
Existen dos ramas, la 1.x y la 2.x. Se pueden [descargar de la web de jQuery](http://www.jquery.com/download) 

¿Cuáles son las diferencias? 

- La rama 2.x no es compatible con IE 6-8
- La rama 2.x es algo más ligera


¿Qué rama utilizamos?

- En principio se pensó que la rama 2.x podría tener mucho menos peso, al quitar dependencias con navegadores antiguos. Sin embargo, surgieron dependencias con los navegadores de los móviles y la ganancia en kilobytes no fue significativa, en torno a un 10%.

- Por otra parte [el porcentaje de usuarios con versiones 6, 7 y 8 de Internet Explorer](http://gs.statcounter.com/) es muy bajo.


Una vez seleccionada la rama hay que elegir si queremos la versión de desarrollo o la versión de producción.

- **Versión de producción**
  - El fichero tiene el sufijo min: jquery-2.2.3.min.js
  - Está comprimida (*minified*)
  - Aproximadamente 90KB
- **Versión de desarrollo**
  - Sin comprimir
  - Aproximadamente 3 veces más pesada, en torno a 270KB


## Cuando llamar a jQuery
- En la parte superior de la página (head):
  - **Siempre después de los estilos**
  - Antes de ser utilizado por cualquier otro script o dependencia
      ```	
      <script type="text/javascript" src="jquery-1.10.2.min.js"></script>
      ```
    
- En la parte inferior de nuestra página:
  - Mejor, porque se optimiza la carga de la página
  - Antes de ser utilizado por cualquier otro script o dependencia


## CDN
CDN son las siglas de *Content Delivery Network*. Son un grupo de servidores repartidos por todo el mundo en puntos estratégicos y pensados para la distribución de ficheros.

Cuando contratamos un hosting para alojar un sitio web, es habitual que nos oferten el uso de algún CDN para colgar principalmente contenido estático. 


### Ventajas de usar un CDN
- Permite al navegador realizar más peticiones http en paralelo (distintos dominios)
- Posibilita la descarga del contenido desde un servidor más cercano (menor latencia).

Para las librerías más conocidas es frecuente que empresas como Google o Microsoft nos ofrezcan sus CDNs.


### CDN para jQuery

```	
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>

	<script type="text/javascript" src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js"></script>
    
	<script type="text/javascript" src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
    ```

Si el usuario navegada por varias página que utilizan el mismo CDN (mismo src),solo lo descarga una vez, ya que podrá usar la caché del navegador.


## Ejecución del código
Si analizamos la carga de un sitio web mediante Chrome Developer Tools, veremos (pestaña Network o Timeline), dos rayas verticales azul y roja. La raya azul corresponde a la carga del DOM de la página y la roja al evento de load de la página.

El evento load siempre es posterior: una vez cargado todo el DOM puede ser que se deba cargar el contenido de algún iframe, banner de anuncios, imágenes...

Casi siempre que utilizamos jQuery nos hace falta acceder a algún elemento de nuestra página. ¿Cómo hacemos para asegurarnos de que dicho elemento ya está cargado?


### Mediante JavaScript
```
window.onload = function(){ /*Aquí viene mi código de javascript*/ }
```
Aunque mi código esté situado en el head de la página, no se ejecutará mi función hasta que se produzca el evento load de la página.
Ventajas:
- El DOM ya está cargado, no tendremos errores.
Desentajas:
- Puede que tarde mucho en ejecutarse nuestro código en JavaScript, por ejemplo si hay imágenes pesadas o la conexión es lenta.


**Actividad**

Crea una página web con un enlace que muestre un alert con el texto "Hola Mundo" y que "anule" el enlace.


**Solución**
``` 
<!DOCTYPE html>
 <html>
 <head>
   <meta charset="utf-8">
   <title>Hola Mundo en javaScript</title>
   <script type="text/javascript">
   window.onload = function() { 
   		document.getElementById("holamundo").onclick = holaMundo;
   }
   function holaMundo()
   {
	   alert ("Hola Mundo");
	   return false;
   }
   </script>
 </head>
 <body>
   <a id="holamundo" href="http://jquery.com/">jQuery</a>
 </body>
 </html>
```


### Mediante jQuery
jQuery define un nuevo evento, el evento ready para el documento html. El evento ready se produce cuando el DOM está cargado, aunque no estén renderizados algunos elementos de la página. ¡Ojo al efectuar acciones sobre imágenes si no están todavía cargadas!

```
$(document).ready(function(){
   // Aquí viene mi código jQuery o JavaScript
});
```


**Actividad**

Descarga una versión de jQuery e inserta las siguientes instrucciones de jQuery:
```
		$("a").click(function(event) {
			alert("Hola Mundo");
			event.preventDefault();
		});
```


**Solución**
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Hola Mundo con jquery</title>
<script src="jquery-1.10.2.min.js"></script>
<script>
	$(document).ready(function() {
		$("a").click(function(event) {
			alert("Hola Mundo");
			event.preventDefault();
		});
	});
</script>
</head>
<body>
	<a href="http://jquery.com/">jQuery</a>
</body>
</html>
```



## Sintaxis de jQuery
En una expresión de jQuery hay 3 partes:
- **$**: para cargar jQuery
- **(selector)**: para seleccionar uno o varios elementos del DOM en base a sintaxis de CSS
- **.action()**: Acción que se ejecuta sobre los elementos seleccionados del DOM


### Ejemplos de uso del selector de jQuery
```
$(this).hide() 		//oculta el elemento actual
$("p").hide() 		//oculta todos los elementos de tipo párrafo
$("p.test").hide() 	//oculta todos los párrafos con class=test
$("#test").hide() 	//oculta todos los elementos con id=test
$("p")  //se seleccionan todos los elementos de tipo párrafo
$("p.intro")  //todos los párrafos con class=intro
$("p#demo")  //todos los párrafos con id=demo
$("[href]") //todos los elementos con atributo href
$("[href='#']") //todos los elementos con atributo href="#"
$("[href!='#']")  //todos los elementos con atributo href diferente de "#"
$("[href$='.jpg']") //todos los elementos con atributo href que acabe en .jpg
$("p").css("background-color","yellow"); //modificamos el background-color de todos los párrafos a amarillo
$("p#intro:first") 	//El primer párrafo con id="intro"
$("ul li:first") 	El primer elemento <li> de cada <ul>
$("div#intro .head") //Todos los elementos con class="head" dentro de un <div> con id="intro"
```


### Conflictos con otras librerías
* Utilizamos jQuery.noConflict() para evitar conflictos de nombre con otras librerías de JavaScript que puedan utilizar también la variable *$*.

  ```
  <!DOCTYPE html>
    <html>
      <head>
        <script src="jquery.js"></script>
      <script>
        var jq=jQuery.noConflict();
        jq(document).ready(function(){
          jq("button").click(function(){
            jq("p").hide();
          });
        });
      </script>
    </head>
    <body>
      <p>Esto es un párrafo.</p>
      <button>Pulsa aquí</button>
    </body>
  </html>

  ```
  
  
  # Efectos
Son una forma muy visual para entrar en contacto con dos características muy importantes en jQuery:
- Las **funciones de callback**
- La **concatenación de métodos**


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
Para ver todas las opciones de efectos consulta la [api de efectos de jquery](http://api.jquery.com/category/effects/)


### Parámetros de las funciones
- El primer parámetro nos indica la velocidad y puede tener los valores: slow, fast, normal o milisegundos.
- El segundo parámetro es la función que hay que ejecutar en el momento en que se complete la acción de hide o show.
- Los parámetros son opcionales


### Función animate
- Con la función animate, podemos hacer efectos más complejos:
  - Con valores absolutos o relativos
  - Si ponemos varios animates seguidos, los irá encolando (no empezará una instrucción hasta terminar la anterior).
```
$(selector).animate({
      left:'250px',
      opacity:'0.5',
      height:'150px',
      width:'150px'
    });
```


- El siguiente ejemplo se ejecutará cuando hagamos clic en el botón:

  ```
  $("button").click(function(){
    $("div").animate({
      left:'250px',
      height:'+=150px',
      width:'+=150px'
    });
  });
  ```

- Pararemos una animación mediante la función stop:
```
$(selector).stop(stopAll,goToEnd);
```


## Funciones de callback
**JavaScript es asíncrono**. Como en otros lenguajes, se ejecutan las instrucciones línea a línea. Sin embargo puede ser que una sentencia no haya terminado su ejecución y ya haya comenzado la siguiente:

```
$("p").hide(1000);
alert("El párrafo se ha escondido ¿AHORA?");
```


En JavaScript las funciones son [ciudadanos de primer orden](http://ryanchristiani.com/functions-as-first-class-citizens-in-javascript/) y se pueden pasar como parámetros. Para evitar el comportamiento asíncrono entre las dos instrucciones anteriores, pasaremos la segunda instrucción como parámetro de la función hide. Para hacer esto tendremos que embeberla en una función:

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



# html y jQuery


## Manipulación del contenido html
- Cambia el contenido del elemento/s html seleccionado/s:
```
$(selector).html(contenido)
```
- Añaden contenido en el elemento HTML seleccionado:
```
$(selector).append(content)
$(selector).prepend(content)
```
- Añaden contenido después o antes del elemento HTML seleccionado:
```
$(selector).after(content)
$(selector).before(content)
```


## Manipulación de atributos de html

- Método **attr()**
  - Obtenemos los valores de los atributos de las etiquetas html:
  
  ```
  //obtenemos el valor del título del enlace:
  $("a").attr("title");
  ```

  - Si hay varios atributos se pueden recorrer mediante el método each():
  ```
    $("a").each(function(i){
        var titulo = $(this).attr("title");
        alert("Atributo title del enlace " + i + ": " + titulo);
     });
  ```
  - Podemos modificar también el valor de los atributos pasando un segundo parámetro:

    ```
    //modificamos el atributo title:
    $("a").attr("title", "Mi nuevo título");
    ```


- Método **prop()**

```
$(elemento).prop("checked", true);
```
- ¿Cuándo usar attr() y cuando prop()?
  - Atributos que se modifican con attr(): class, id, href, label, src, title...
  - Propiedades que se modifican con prop(): autofocus, checked, async, multiple, readOnly...


## Manipulación de css
- Obtiene la propiedad CSS del primer elemento seleccionado:
```
//$(selector).css(name) 	
$(this).css("background-color"); 
```

- Establece el valor de una propiedad CSS de los elementos seleccionados:
```
//$(selector).css(name,value) 	
$("p").css("background-color","yellow"); 
```
- Establece varias propiedades CSS de los elementos seleccionados:
```
//$(selector).css({properties}) 
$("p").css({"background-color":"yellow","font-size":"200%"}); 
```

- Establece la altura de los elementos seleccionados:
```
//$(selector).height(value) 	
$("#div1").height("200px"); 
```

- Establece la anchura de los elementos seleccionados:
```
//$(selector).width(value) 	
$("#div2").width("300px");
```


## Formularios
- Función **val()**: para obtener los valores de los elementos o inicializarlos.
```
/*Inicializamos la caja de texto y luego guardamos su contenido en una variable*/
$("textarea").val("Esto es una caja de texto");
var texto = $("textarea").val();
```
- En caso de inicializar varios valores a la vez (por ejemplo un select múltiple), los pondremos entre corchetes:
```
$("select").val(["Pedro", "Juan", "Miguel"]);
</source>
```

- Función **text()**: Obtiene o establece el contenido de los elementos seleccionados.
  - Es parecida a html(), pero obtendremos solo texto, sin etiquetas:
  
    ```
    <!DOCTYPE html>
      <html>
        <head>
          <script src="jquery.js"></script>
          <script>
            $(document).ready(function(){
              $("#btn1").click(function(){
                alert("Text: " + $("#test").text());
              });
              $("#btn2").click(function(){
                alert("HTML: " + $("#test").html());
              });
            });
          </script>
        </head>
        <body>
          <p id="test">Texto con <b>negrita</b></p>
          <button id="btn1">Ver texto</button>
          <button id="btn2">Ver html</button>
        </body>
      </html>

    ```



# Ajax


## JSON
- JavaScript Object Notation
- Se utiliza para almacenar e intercambiar información
- Más pequeño que XML y más rápido y sencillo de analizar (parsear).
- Se basa en la sintaxis del propio JavaScript para objetos. 

```
//Objeto JSON:
{ "nombre":"Pepe" , "apellido":"Pérez" }
```


- Otros ejemplos:
```
//Array JSON
{
"estudiantes": [
    { "nombre":"Juan" , "lastName":"Alcocer" }, 
    { "nombre":"Ana" , "lastName":"Serrano" }, 
    { "nombre":"Mario" , "lastName":"Gil" }
  ]
}
//sintáxis en JavaScript:
var estudiantes = [
    { "nombre":"Juan" , "lastName":"Alcocer" }, 
    { "nombre":"Ana" , "lastName":"Serrano" }, 
    { "nombre":"Mario" , "lastName":"Gil" }
  ];
```


## ¿Qué es AJAX?
- AJAX quiere decir **Asynchronous JavaScript and XML**.
- Sirve para cargar datos en background y mostrarlos en la web sin necesidad de recargar la página, por eso lo de asíncrono.
- XHR significa **XML HTTP REQUEST** y es hablar de lo mismo. 
- Lo podemos ver en el inbox de gmail, en google maps cuando aplicamos el zoom, etc.
- jQuery y AJAX:
  - La implementación de AJAX es distinta en función del navegador.
  - Facilita la sintaxis para usar AJAX


- Cachear AJAX
```
$.ajaxSetup ({  
    cache: false  
});  
```
- Será útil usar caché solamente con contenidos estáticos.
- Es aconsejable indicarlo porque el comportamiento por defecto puede variar en función del navegador.
- La caché solo funciona mediante GET.


## Método load
- Es el método más sencillo. Lo usaremos para cargar cierto contenido por AJAX al DOM de la página actual.
```
$(selector).load(URL,data,callback);
```


**Ejemplo de uso**
- Petición de contenido vía ajax al pulsar un enlace:

```
 <html>
<head>
   <title>Ajax Simple</title>
<script src="jquery-1.8.2.min.js" type="text/javascript"></script>   
<script>
$(document).ready(function(){
   $("#enlaceajax").click(function(evento){
      evento.preventDefault();
      $("#destino").load("contenido-ajax.html");
   });
})
</script>
</head>
<body>

<a href="#" id="enlaceajax">Haz clic!</a>
<br>
<div id="destino"></div>

</body>
</html>
```


### Seleccionar datos en petición AJAX
- Podemos añadir un selector jQuery a nuestra URL de petición AJAX:
```
$("#div1").load("mipagina.html #p1");
```
- En este caso obtendremos del fichero mipagina.html el elemento identificado con id="p1".


### Paso de parámetros
- El método load puede llevar parámetros o una función de callback:
```
$(document).ready(function(){
   $("#enlaceajax").click(function(evento){
      evento.preventDefault();
      $("#destino").load("recibe-parametros.php", {nombre: "Pepe", edad: 45}, function(){
         alert("recibidos los datos por ajax");
      });
   });
})
```


- Fichero en php:
```
Recibido el siguiente dato:
<br/>
Nombre: <?php echo $_POST["nombre"];?>
<br/>
Edad: <?php echo $_POST["edad"];?>
```


### Con mensaje de "carga"
```
$(document).ready(function(){
   $("#enlaceajax").click(function(evento){
      evento.preventDefault();
      var ajax_load = "<img src='img/load.gif' alt='loading...' />";  
      var loadUrl = "pagina_lenta.php";  
      $("#result").html(ajax_load).load(loadUrl);  
   });
})
```


- Fichero en php:
```
<?php
sleep(3);
echo ("He tardado 3 segundos en ejecutar esta página...");
?>
```


### Uso del callback

```
$(selector).load(URL,data, callback);
```
- El parámetro opcional de callback especifica la función de callback a ejecutar cuando el método load() se haya completado. Puede tener varios parámetros:
  - responseTxt - contiene el resultado de la llamada si ha sido un éxito
  - statusTXT - contiene el estado de la llamada
  - xhr - contiene el objeto XMLHttpRequest


- Ejemplo de uso:

```
$("button").click(function(){
  $("#div1").load("demo_test.txt",function(responseTxt,statusTxt,xhr){
    if(statusTxt=="success")
      alert("External content loaded successfully!");
    if(statusTxt=="error")
      alert("Error: "+xhr.status+": "+xhr.statusText);
  });
});
```


## Otros métodos
- **$.getJSON()**: Obtiene un fichero JSON de un sitio remoto
- **$.getScript()**: Obtiene un fichero javascript de un sitio remoto
- **$.get()**: hace peticiones ajax vía GET 
- **$.post()**: hace peticiones ajax vía POST
- **$.ajax()**: De más bajo nivel. Será útil para controlar errores en las peticiones AJAX o alguna función específica de AJAX (por ejemplo la cache).



## Ajax y Firebug
- Podemos hacer un seguimiento de las peticiones Ajax desde la pestaña de Red de Firebug, opción XHR (XML HTTP REQUEST):

![](Firebug_load_1.png)


- Si pulsamos en el recuadro del + a la izquierda, podremos ver los parámetros que se envían en la petición AJAX. En esta petición no hay ningún parámetro. El único que hay es un número aleatorio generado para forzar que la petición no se sirva de la caché.

![](Firebug_load_2.png)


- En la pestaña de respuesta (response) encontramos lo que devuelve la petición AJAX:

![](Firebug_load_3.png)


- En este caso enviamos más de un parámetro vía GET. Para pasar más de un parámetro:
```
	$("#load_get").click(function(){
		$("#result")
			.html(ajax_load)
			.load(loadUrl, "language=php&version=5");
	});
```

![](Firebug_load_4.png)


- Si pasamos los parámetros como un objeto en vez de como una cadena, se enviarán vía POST:
```
	$("#load_post").click(function(){
		$("#result")
			.html(ajax_load)
			.load(loadUrl, {language: "php", version: 5});
	});
```

![](Firebug_load_5.png)



## Método .ajax
- Utilizaremos ajax mediante el plugin jQuery de Sublime
- Tan solo con escribir *ajax* dispondremos del snippet de Sublime:

```
$.ajax({
  url: '/path/to/file',
  type: 'default GET (Other values: POST)',
  dataType: 'default: Intelligent Guess (Other values: xml, json, script, or html)',
  data: {param1: 'value1'},
})
.done(function() {
  console.log("success");
})
.fail(function() {
  console.log("error");
})
.always(function() {
  console.log("complete");
});
```


- Podemos optar por [utilizar **promesas**](http://www.formandome.es/javascript/promises-y-deferreds-en-jquery/) si la lectura asíncrona del código es complicada
