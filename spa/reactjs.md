# React.js
- Desarrollado por facebook y utilizado en su sitio web
- Instagram está realizado completamente con React
- Sirve para simplificar el diseño de interfaces de usuario complejas

## Requisitos
- JavaScript
- npm
- ES2015

## Componentes
- React se basa en componentes
    - Utilizaremos clases de JavaScript (ES2015)
    - Si un componente es complejo se divide en componentes más simples
- Cada componente es como una función:
    - Genera una salida cuando se ejecuta: método render()
    - La ejecución se produce sobre un **dom virtual**

## Virtual Dom
- Permite que React sea muy rápido
- React utiliza el DOM Virtual para hacer los mínimos cambios posibles en el DOM real
    - La renderización en el navegador es mucho más rápida
    - Se ejecuta un diff entre el dom virtual y el dom real y se actualizan solo las diferencias. 
 
## Primeros pasos
- Aunque no es lo habitual en los tutoriales de React:
    - Vamos a partir de un escenario con Webpack
        - Utilizaremos un [starter kit](https://github.com/gaearon/react-hot-boilerplate):
        - Evitamos la configuración de webpack que suele ser compleja

    - [Añadiremos snippets a Sublime](https://github.com/juanda99/react-v0.14-snippets) para poder trabajar con React más rápido

## Hola Mundo
- Clonamos el starter kit, instalamos dependencias y lo editamos
```
git clone https://github.com/gaearon/react-hot-boilerplate
cd react-hot-boilerplate
npm install
subl .
```
- Cambiamos el texto en *src/app.js* y comprobamos que cambia de forma automática
- Añade un párrafo. ¿Qué ocurre?

## JSX
- JSX = JavaScript XML
- Todo lo que devuelve el método render se escribe en JSX
- Conseguimos código html legible (sin comillas) dentro de js
- ¿Mezclamos JavaScript con html?
    - ... y dentro de poco también CSS
    - Si, no pasa nada: **<App />** es un componente web 

## ¿Mezclamos todo?

- **render** debe devolver un único elemento html
- El atributo **class** de html es una palabra reservada de JavaScript, por lo que en JSX se utiliza **className**
- Las variables en JSX se ponen mediante llaves

``` 
import React, { Component } from 'react';

export default class App extends Component {
  render() {
    var respuesta = 'Hola, ¡buenos días!'
    return (
      <div>
        <h1>Hola Mundo</h1>
        <p className="rojo">{respuesta}</p>
      </div>
    );
  }
}
```

## Funcion map
- Es bastante habitual utilizar la función map cuando manejamos arrays:

```
import React, { Component } from 'react';

export default class App extends Component {
  render() {
    const famosos = [ 'Oliver Khan', 'Albert Einstein' ]
    return (
      <div>
        {famosos.map(famoso => <h1>{famoso}</h1>)}
      </div>
    );
  }
}
```

** Ejercicio:**
- ¿Cómo implementarías el método render si además de los famosos tuvieras que mostrar sus comentarios?
- Utiliza como ejemplo este array de objetos:
```
var comentarios= [
  {autor: 'Oliver Khan', frase: 'Ultimamente veo más los abdominales de Cristiano Ronaldo que los pechos de mi mujer'},
  {autor: 'Albert Einstein', frase: 'Dos cosas son infinitas: el universo y la estupidez humana; y yo no estoy seguro sobre el universo'}
    ]
```

**Solución:**
```
import React, { Component } from 'react';

export default class App extends Component {
  render() {
    var comentarios= [
      {autor: 'Oliver Khan', frase: 'Ultimamente veo más los abdominales de Cristiano Ronaldo que los pechos de mi mujer'},
      {autor: 'Albert Einstein', frase: 'Dos cosas son infinitas: el universo y la estupidez humana; y yo no estoy seguro sobre el universo'}
    ]
    return (
      <div>
        {comentarios.map(comentario => <div><h1>{comentario.autor}</h1><p>{comentario.frase}</p></div>)}
      </div>
    );
  }
}
```

## Comunicación entre componentes
Vamos a hacer algo similar al ejercicio anterior pero con nuestras cervezas. Lo primero es carga el fichero cervezas.json y renderízarlo en un navegador. Para poder cargar el fichero cervezas.json desde nuestro JavaScript tendremos que configurar Webpack:
  - Instalamos un loader de json para webpack:
```
npm i -D json-loader
```
  - Configuramos Webpack para que utilice el loader:
  ```
  module.exports = {
  ...
      module: {
          loaders: [
              { test: /\.json$/, loader: "json-loader" }
          ]
      }
  }
  ```
  - Por último escribimos nuestro componente, modificando ligeramente el del ejercicio anterior:

    ```
    import React, { Component } from 'react'
    export default class App extends Component {
      render() {
        var cervezas = require('./cervezas.json')
        return (
          <div>
            <h1>Mi lista de cervezas</h1>
            {cervezas.map(cerveza => <div><h2>{cerveza.Nombre}</h2><p>{cerveza.Envase}</p></div>)}
          </div>
        );
      }
    }
```

Si vemos en la consola del navegador, observaremos un error que luego solucionaremos: 

```Warning: Each child in an array or iterator should have a unique "key" prop. Check the render method of `App`.```

Cada elemento del DOM virtual puede corresponder a un elemento del DOM real y la forma de conseguir la trazabilidad es mediante la propiedad key.

Intentemos ahora hacer una cosa en la que React es muy bueno: simplificando código, haciendo las cosas sencillas. Ahora mismo nuestro código tiene dos pegas:
- Nuestra clase App define la renderización de las cervezas:
  - Debería indicar que hay que renderizar cervezas
  - Otra clase llamada Cerveza debería ser la que tuviera los detalles de como renderizarlas.
- El código se ve algo complejo, quizá mejore al crear la clase Cerveza, pero podéis pensar además que se mezcla el código js con el código en html de forma que queda poco legible.


### Creamos el componente Cerveza
Pensando en componentes, ahora mi class App representa una lista de cervezas. La renderización de cada cerveza puede ser muy simple o muy compleja. Quizá nos interese tener una clase específica para representarla: 

  ```
  import React, {Component, PropTypes} from 'react'

  export default class Cerveza extends Component {


    render() {
      return (
        <div id={this.props.key}>
          <h1>Marca: {this.props.marca}</h1>
          <p>Envasado: {this.props.envase}</p>
        </div>
      )
    }
  }
  ```

 - En el código de la App llamaremos a la clase:

  ```
  import React, { Component } from 'react';
  import Cerveza from './Cerveza.js'
  export default class App extends Component {
    render() {
      var cervezas = require('./cervezas.json')
      return (
        <div>
          {cervezas.map(cerveza => <Cerveza key={cerveza.Nombre} marca={cerveza.Nombre} envase={cerveza.Envase}/>)}
        </div>
      );
    }
  }
  ```

- Organizando un poco el código de la App:

  ```
  import React, { Component } from 'react';
  import Cerveza from './Cerveza.js'
  export default class App extends Component {
    getCervezas() {
      var cervezas = require('./cervezas.json')
      return cervezas.map(cerveza =><Cerveza key={cerveza.Nombre} marca={cerveza.Nombre} envase={cerveza.Envase}/>)
    }
    render() {
      let cervezas = this.getCervezas()
      return (
        <main>
          <h1>Mi lista de cervezas</h1>
          {cervezas}
        </main>
      );
    }
  }
  ```
  
  Algunos detalles del código:
  - La función getCervezas debería ser una llamada Ajax al servidor
  - Las propiedades de la clase Cerveza las mandamos mediante atributos html
  - La clase Cerveza accede a sus atributos mediante *this.props* y puede comprobar el tipo de datos recibidos mediante:
```
    static propTypes = {
      marca: PropTypes.string,
      envase: PropTypes.string,
      key: PropTypes.string
  }
```

