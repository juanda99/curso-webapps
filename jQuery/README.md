
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
- En la parte superior de la página (dentro del head):
  - **Siempre después de los estilos**
  - Antes de ser utilizado por cualquier otro script o dependencia
  
    ```	<script type="text/javascript" src="jquery-1.10.2.min.js"></script>```   
- En la parte inferior de nuestra página:
  - Mejor, porque se optimiza la carga de la página
  - Antes de ser utilizado por cualquier otro script o dependencia


## Uso de un CDN
CDN son las siglas de *Content Delivery Network*. Son un grupo de servidores repartidos por todo el mundo en puntos estratégicos y pensados para la distribución de ficheros).

Cuando contratamos un hosting para alojar un sitio web, es habitual que nos oferten el uso de algún CDN para colgar principalmente contenido estático. Las ventajas son las siguientes:
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


