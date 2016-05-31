# JavaScript en servidor
## Ventajas
- En el servidor Node.js también es single-threaded
- Ya hemos visto que JavaScript es asíncrono y eso es una gran ventaja.
- Al contrario que en el navegador, encontramos muchas llamadas asíncronas: 
    - Llamadas a APIs
    - Lectura y escritura de ficheros
    - Ejecución de cálculos en el servidor
    - ....
- Llamadas síncronas en servidor serían fatales:
    - ¡Bloqueariamos las conexiones al servidor hasta que acabase la instrucción bloqueante!

{%youtube%}9nPdNyMbpSk{%endyoutube%}

{%m id="dQw4w9WgXcQ", m=14, s=47%}Ver parte interesante del video{%endm%}

## CallbackHell
- Imagina que guardamos un registro de los accesos de los usuarios a nuestra app:

```
trackUser =  function(userId) {
  users.findOne({userId: userId}, function(err, user) {
    var logIn = {userName: user.name, when: new Date};
    logIns.insert(logIn, function(err, done) {
      console.log('wrote log-in!');
      });
  });
```

- Tenemos 3 funciones anidadas en una simple operación.
- Esto es lo que se conoce como [callback hell](https://strongloop.com/strongblog/node-js-callback-hell-promises-generators/)

## Evitar el callback en el navegador
- Mediante el [uso de promesas](https://www.promisejs.org/)
- Se trata de escribir código asíncrono con un estilo síncrono.
- Opciones más actuales:
    - Generators / Yields (ES6)
    - Async / Await (ES7)
    - El soporte de ES6 en node es limitado (--harmony) y también en el navegador => TRANSPILERS (babel)
- Ver [comparativa de métodos asíncronos](https://thomashunter.name/blog/the-long-road-to-asyncawait-in-javascript/)

