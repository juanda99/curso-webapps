# React.js con material-ui

## Rutas y arquitectura de la aplicación
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
- Creo una carpeta llamada *layout* donde colocaremos el footer, header y resto de componentes asociados a la plantilla. De momento la plantilla con el siguiente código:

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

## Integración con material-ui
- Lo primero que debemos hacer es [instalar y configurar material-ui](http://www.material-ui.com/#/get-started/installation) para el uso en nuestra aplicación: 
``` 
npm i -S material-ui react-tap-event-plugin
```

- En el fichero *app.js*:

  ```
  import injectTapEventPlugin from 'react-tap-event-plugin';

  // Needed for onTouchTap
  // Check this repo:
  // https://github.com/zilverline/react-tap-event-plugin
  injectTapEventPlugin();
  ```
- En el index.html:
```
<link href='https://fonts.googleapis.com/css?family=Roboto:400,300,500' rel='stylesheet' type='text/css'>
```

- Comprobamos si funciona o no, mediante un *npm start* y vemos que los warnings que nos han salido en la instalación hay que arreglarlos:  ciertos errores de dependencias que nos obligan a actualizar la versión de *react* y *react-dom*

Creo el componente *Menu.js* copiando código de la web de Material-ui:

  ```
  import React from 'react'
  import Drawer from 'material-ui/Drawer'
  import MenuItem from 'material-ui/MenuItem'
  import RaisedButton from 'material-ui/RaisedButton'

  export default class Menu extends React.Component {

    constructor(props) {
      super(props);
      this.state = {open: false};
    }

    handleToggle = () => this.setState({open: !this.state.open});

    render() {
      return (
        <div>
          <RaisedButton
            label="Toggle Drawer"
            onTouchTap={this.handleToggle}
          />
          <Drawer open={this.state.open}>
            <MenuItem>Menu Item</MenuItem>
            <MenuItem>Menu Item 2</MenuItem>
          </Drawer>
        </div>
      )
    }
  }
  ```

- En la template lo tengo que llamar:

  ```
  import React, {Component} from 'react'
  import Menu from './Menu.js'

  export default class Template extends Component {
    render() {
      return (
        <div>
          <header><h1>Sitio web de mis cervezas</h1></header>
          <Menu/>
          <main>{this.props.children}</main>
          <footer>Realizado por juanda</footer>
        </div>
      )
    }
  }
  ```

- Comprobamos que no funciona ya que para  usar los componentes de Material-ui es necesario utilizar un theme. Lo añadimos [tal y como marca la documentación](http://www.material-ui.com/#/get-started/usage), en el fichero *App.js*:

```
import React, { Component } from 'react'
import { Router, Route, browserHistory, IndexRoute } from 'react-router'
import Index from './views/Index'
import Contactar from './views/Contactar'
import Cervezas from './views/Cervezas'
import Template from './layout/Template'

import getMuiTheme from 'material-ui/styles/getMuiTheme';
import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';

import injectTapEventPlugin from 'react-tap-event-plugin'

  // Needed for onTouchTap
  // Check this repo:
  // https://github.com/zilverline/react-tap-event-plugin
injectTapEventPlugin()

export default class App extends Component {
  render() {
    return (
      <MuiThemeProvider muiTheme={getMuiTheme()}>
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
      </MuiThemeProvider>    
    )
  }
}
```
- Si lo ejecutamos ahora veremos que funciona. Sin embargo el botón queda escondido detrás del menú. Lo podemos arreglar utilizando css directamente desde el JavaScript:

```
import React from 'react'
import Drawer from 'material-ui/Drawer'
import MenuItem from 'material-ui/MenuItem'
import RaisedButton from 'material-ui/RaisedButton'

const styles = {
  container: {
    width:'800px',
    margin: '0 auto'
  }
}

export default class Menu extends React.Component {

  constructor(props) {
    super(props);
    this.state = {open: false};
  }

  handleToggle = () => this.setState({open: !this.state.open});

  render() {
    return (
      <div style={styles.container}>
        <RaisedButton
          label="Toggle Drawer"
          onTouchTap={this.handleToggle}
        />
        <Drawer open={this.state.open}>
          <MenuItem>Menu Item</MenuItem>
          <MenuItem>Menu Item 2</MenuItem>
        </Drawer>
      </div>
    )
  }
}
```
## Más tareas
- Podríamos añadir otros componentes pero la tarea no deja de ser similar.
- Quizá podríamos utilizar un sistema de rejilla tipo Bootstrap para colocar los elementos y ahorrarnos código css o js. Una buena opción sería http://flexboxgrid.com/.
- Y podemos utilizar componentes externos o incluso combinarlo con nuestros elementos de Material-ui.
- 

