# Linters en JavaScript
- Herramientas que realizan la lectura del código fuente
  - Detectan errores/warnings de código
    - Variables sin usar o no definida, llave sin cerrar...
  - Detectan fallos de estilo
    - Comillas dobles en vez de simples, espacios en vez de tabulaciones...


## JSLint
- JSLint es un analizador online de código javaScript creado por Douglas Crockford 
- Los criterios evaluados corresponden a los que marcó su creador 
    - Demasiado estricto
    - No es configurable o extensible


## JSHint
    - Fork de JSLint
    - El objetivo de JSHint es no imponer un convenio particular
    - La gente utiliza diferentes estilos y convenciones.
    - El linter debe adaptarse al desarrollador y no al revés


## JSCS
    - Solo para verificar el estilo del código
    - Tiene muchas reglas. No hace falta defirlas, podemos utilizar un [preset](https://github.com/jscs-dev/node-jscs/tree/master/presets)


## ESLint
    - El último en llegar (2013), recoge lo bueno de los anteriores
    - Podemos [fijar nuestras reglas](http://eslint.org/docs/rules/) e incluso luego cambiar nuestro estilo (--fix)
    - Y además tiene soporte para ES6 y para JSX (que se usa en React)
    - Será el que usemos :-)