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