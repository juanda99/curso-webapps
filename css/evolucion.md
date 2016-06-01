# Evolución del CSS



## Origen del css

- Se inventó parar la presentación del marcado **semántico** (html 5)
- Ejemplo en [CSS Zen Garden](http://www.csszengarden.com/)
- Fue un cambio radical en los tiempos en que los layouts estaban basados en tablas


## Documentos vs Webapps
- Cuando pensamos en sitios web sencillos, tenemos un *pensamiento global* para todas las páginas:
    - Mismo header, footer, tipo de lista, párrafos...
    - A todas las páginas se les aplican los mismos estilos
    - El global scope o ámbito global del CSS tiene sentido
- Si nuestro sitio se vuelve complejo la cosa cambia:
    - El global scope y un mantenimiento fácil dejan de ser sinónimos
    - Es lo mismo que pasa en un lenguaje de programación con los ámbitos de las variables


## Forma clásica de hacer CSS
- Como el CSS tiene ámbito global: 
  - Las clases css que definimos puden provocar estilos no deseados en algún componente.
  - Puede haber incompatibilidades entre dos componentes (clases coincidentes)
  - Tendremos que utilizar selectores suficientemente específicos para evitar ese tipo de errores. Se opta por diversas soluciones como OOCSS (Object CSS) y BEM:
  - 
```
.Block__Element--Modifier {....}
```


### Ejemplo de BEM
- Se usa en Material design:

    ```
    <ul class="menu">
      <li class="menu__item">
        <a class="menu__link">
          <span class="menu__text"></span>
        </a>
      </li>
    </ul>
    ```


- La metodología es utilizar selectores que sean fáciles de reusar, como es el selector *class*. Ponemos ciertas restricciones a nuestro uso de CSS:

  ```
  /* BIEN */
  .alert {
      font-weight: bold;
  }
  .danger {
      color: red;
  }
  /* MAL, menos reusable */
  .alert.danger {
      font-weight: bold;
      color: red;
  }
  ```

- Separar el contenedor del contenido (los containers no tienen que tener estilos visuales, lo que sería el theme)


### Ejemplo con Bootstrap
- Ejemplo típico de OOCSS. Se usan numerosas clases:
```
btn
btn-default, btn-primary, btn-success....
btn-lg, btn-sm, btn-xs
disable, active
```
- Se utiliza un grid system con o sin media queries
- Layout helpers (visible-sm...)
- Reglas básicas ¡sin usar clases!
    - Selector de etiqueta (h1, p, a ....)
    - Selector etiqueta con descendente (h1 em)
    - Selector etiqueta con hijo (ul>li)
- Reset de los estilos del navegador
- Normalmente agrupamos estilos por categorías (grid, botones, tipografía, imágenes...)
- Usamos preprocesadores como Less, Sass o Stylus.



## Web Components
- Van a llegar los web components al browser... aunque ya tiene algunos:

```
<select>
   <option>....</option>
   <option>....</option>
</select>

<input type="date" />
```


### Situación actual

- Polymer crea polyfills para que se puedan usar
- Angular tiene sus directives
- React es el que "tiene el mercado" desde el 2015:
    - Todo son componentes
    - No hay otro tipo de elementos como controllers


### Directrices para hacer web components
- Las imágenes que usa el componente pertencen al componente
- El css que usa el componente pertenece al componente
- No nos interesan los detalles de implementación del web component (ej. datepicker)


### Web components de terceros
- jQuery UI Date Picker (que horror: ficheros, css...)
- Se automatizan las tareas con herramientas como Grunt o Gulp


### Desarrollo actual de componentes
- Significa pensar en herramientas como webpack que integran imagenes y css dentro del JavaScript:

```
require('./MyComponent.css')
const MyComponent = () => (
  <div className='MyComponent'>
    <div className='MyComponent__Title'>....</div>
       ...
    </div>
  </div>
);
export default MyComponent
```

- Cuando queremos usar el componente todos sus assets nos dan igual:

```
import MyComponent from 'MyComponent';
```



## CSS mediante JavaScript


## Inconvenientes

- Server render CSS: hay que extraer el CSS que genera el JS mediante algún plugin de webpack
  ver: http://stackoverflow.com/questions/34615898/react-server-side-rendering-of-css-modules
- :hover, :focus, :active
- Media queries
- CSS Media queries
- CSS clases for non-js animations

## Vjeux 2014: CSS mediante estilos en JS
- Tabla comparativa: CSS en JS: https://github.com/MicheleBertoli/css-in-js


## CSS Modules
- No queremos hacer CSS con JavaScript

```
import styles from './MyComponent.css'
const MyComponent = () => (
  <div className={styles.header}>
    <div className={styles.title}>....</div>
       ...
    </div>
  </div>
);
export default MyComponent
```

Fichero css:
```
:local (.header) {.....}
:local (.title) {....}
```

- Las clases se convierten en clases únicas globales
- Se evitan colisiones de nombres 
- Se utilizan hashes pero se puede hacer más legible (tipo BEM pero "gratis")
- Como casi todo tiene ambito local se opta porque sea el valor por defecto (así no hay que marcarlo), mediante postcss-local-scope. 
- Configuración webpack: se debe añadir: css-loader?module 

- Composición:

```
.foo {
   composes: heading from '/typography.css';
   composes: box from 'layout.css';
   color: red;
}
```

- @value para colores, media queries...
https://github.com/css-modules/postcss-modules-values

- react-themeable -> styles are props to components
- Radium
- ReactCSSTransitionGroup -> Minuto 31




