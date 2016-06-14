# JavaScript en servidor

![](nodejs.png)


## Qué es nodejs

- NodeJS es un intérprete de JavaScript que se ejecuta en servidor.
- Está basado en el motor de  JavaScript que utiliza Google Chrome (V8), escrito en C++


## Características principales
- Está orientado a eventos y utiliza un modelo asíncrono (propio de JavaScript).
- Al contrario que en el navegador, encontramos muchas llamadas asíncronas: 
    - Llamadas a APIs
    - Lectura y escritura de ficheros
    - Ejecución de cálculos en el servidor
    - ....


- Llamadas síncronas en servidor serían fatales:
    - ¡Bloqueariamos las conexiones al servidor hasta que acabase la instrucción bloqueante!
    - Al ser asíncrono podremos tener muchas sesiones concurrentes


- Es monohilo
   - Utiliza un solo procesador
   - Si queremos usar toda la potencia de la CPU, tendremos que levantar varias instancias de node y utilizar un balanceador de carga ([por ejemplo con pm2](https://github.com/Unitech/pm2))

{%youtube%}9nPdNyMbpSk{%endyoutube%}

Ver la parte interesante del video: {%m id="9nPdNyMbpSk", m=14, s=47%}{%endm%}
   
   
## Desventajas
- Trabajar con código asíncrono hace que a veces el código no sea excesivamente legible
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

