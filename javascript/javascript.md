# Características generales de JavaScript

## Versiones de JavaScript
- **ES5**: 
  - Desde el 2009. 
  - La entienden todos los navegadores.
- **ES6 o ES2015**: 
  - Finalizada en Julio 2015, ¡después de 6 años!
  - [Soporte incompleto por los navegadores](http://kangax.github.io/compat-table/es6/) (hay que usar un transpiler: Babel)
  - [Guía de ES2015](http://babeljs.io/docs/learn-es2015/)
- **ES7** 
  - Ya no se llamará asi
  - Se crean propuestas que se van aprobando y añadiendo al lenguaje.
  - Así tenemos **stages**:
    - Stage 0 - Strawman
    - Stage 1 - Proposal
    - Stage 2 - Draft
    - Stage 3 - Candidate
    - Stage 4 - Finished

- Más info: http://www.2ality.com/2015/11/tc39-process.html

# JavaScript es Single Thread
- Nuestro código se ejecuta en un solo hilo
- Evitamos [típicos errores de la programación multihilo](http://stackoverflow.com/questions/499634/how-to-detect-and-debug-multi-threading-problems)
    - Dificiles de detectar
    - Dificiles de replicar


# LLamadas síncronas o bloqueantes
- Hasta que no acaba una instrucción, no empieza la siguiente
    - [Ver ejemplo](https://jsbin.com/fuzofi/edit?html,console,output)
    - No se ejecuta más JavaScript, en según que casos puede parecer que esté "colgado"
- Normalmente no es problema:
    - Las instrucciones se ejecutan con rapidez (equipos rápidos)
- Pero a veces sí:
    - Llamadas a API
    - Lectura de disco
    - ....

```
<!DOCTYPE html>
<html>
<head>
  <script src="https://code.jquery.com/jquery-1.11.3.js"></script>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JavaScript es single thread</title>
</head>
<body>
  <button>Pulsa aquí </button>
  <script>
    $('button').click(function () {
      var answer = prompt("¿Cómo te llamas?");
      console.log(answer);  
    });
    $('button').click(function () {
      console.log("¡Bienvenido");  
    });
  </script>
</body>
</html>
```

## JavaScript es asíncrono
- Se pude ejecutar una instrucción antes de que acabe la anterior, [Ver ejemplo](https://jsbin.com/hukenok/edit?html,console,output)
- Análisis del ejeemplo:
    - En el event handler hay dos funciones:
        - La primera es asíncrona y no evita que otro código se ejecute en el navegador:
            - ```console.log ("Petición realizada")
            - O la propia renderización en el navegador (css o html)
        - La segunda es una función de callback
            - No se ejecuta hasta que acaba la función asíncrona
- ¡JavaSript no es single thread!
    - Hay un hilo para la ejecución de nuestro software
    - Otro hilo para la gestión interna (avisa de que la llamada asíncrona ha terminado)


``` 
<!DOCTYPE html>
<html>
<head>
  <script src="https://code.jquery.com/jquery-1.11.3.js"></script>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JavaScript: llamadas asíncronas</title>
</head>
<body>
  <button>Pulsa aquí </button>
  <script>
    $('button').click(function() {
      $.get('http://ask.com'), function(data) {
        console.log("Petición contestada", data);
      });
      console.log ("Petición realizada")
    })
  </script>
</body>
</html>
```





- Más info http://egorsmirnov.me/2015/05/22/react-and-es6-part1.html
