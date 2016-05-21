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

## Ejercicio
- ¿Cómo implementarías el método render si además de los famosos tuvieras que mostrar sus comentarios?
- Utiliza como ejemplo este array de objetos:
```
var comentarios= [
  {autor: 'Oliver Khan', frase: 'Ultimamente veo más los abdominales de Cristiano Ronaldo que los pechos de mi mujer'},
  {autor: 'Albert Einstein', frase: 'Dos cosas son infinitas: el universo y la estupidez humana; y yo no estoy seguro sobre el universo'}
    ]
```



