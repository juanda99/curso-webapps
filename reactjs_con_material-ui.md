# React.js con material-ui

## Generar boilerplate
- Hacemos un clone del proyecto e instalamos dependencias:
```
npm install
```

- Instalamos react router:
```
npm i -S react-router
```
- Ahora modificaremos nuestros ficheros fuente. En nuestro componente ```<App/>``` nos encargaremos de renderizar nuestro enrutador (no deja de ser otro componente) que será el que se encargue de cargar las distintas vistas:

  ```
  import React, { Component } from 'react'
  import { Router, Route, browserHistory } from 'react-router'
  import Index from './views/Index'
  import Contactar from './views/Contactar'
  import Cervezas from './views/Cervezas'

  export default class App extends Component {
    render() {
      return (
        <Router history={browserHistory}>
          <Route path="/" component={Index}/>
          <Route path="/cervezas" component={Cervezas}/>
          <Route path="/contactar" component={Contactar}/>
        </Router>
      )
    }
  }
  ```
- Las vistas serán de momento algo tal como:

  ``` 
  import React, {Component} from 'react'

  export default class Cervezas extends Component {
    render() {
      return (
        <h1>Mi lista de cervezas</h1>
      )
    }
  }
  ```

- Vamos a intentar hacer ahora rutas anidadas. En la ruta base, cargaremos una plantilla que será la encargada de colocar el menú, header y footer para todas las páginas:

  ```
  import React, { Component } from 'react'
  import { Router, Route, browserHistory, IndexRoute } from 'react-router'
  import Index from './views/Index'
  import Contactar from './views/Contactar'
  import Cervezas from './views/Cervezas'
  import Template from './layout/Template'

  export default class App extends Component {
    render() {
      return (
        <Router history={browserHistory}>
          <Route path='/' component={Template}>
            /*observa que definimos IndexRoute, que será la ruta por defecto*/
            /*Todas las rutas siguientes están anidadas dentro de template, es decir
            son hijas de la anterior y desde la template cargaremos la que corresponda*/
            <IndexRoute component={Index}/>
            <Route path='cervezas' component={Cervezas}/>
            <Route path='/contactar' component={Contactar}/>
          </Route>
        </Router>
      )
    }
  }
  ```
- Creo una carpeta llamada *layout* donde colocaremos el footer, header y resto de componentes de la plantilla. De momento la plantilla con el siguiente código:

```
import React, {Component} from 'react'

export default class Template extends Component {
  render() {
    return (
      <div>
        <header><h1>Sitio web de mis cervezas</h1></header>
        <main>{this.props.children}</main>
        <footer>Realizado por juanda</footer>
      </div>
    )
  }
}
```



