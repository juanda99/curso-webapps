# Proyecto Web básica

## Generación del código html del sitio
De aquí en adelante utilizaremos emmet para producir de forma rápida el código html del sitio. 

### Código html común
- Creamos la estructura de directorios para la aplicación (css, imágenes).
- Creamos el primer fichero y generamos el código común con el resto de las páginas del sitio (básicamente todo menos la parte central). No te olvides de **marcar previamente el fichero como html para que Emmet funcione**
- Esqueleto html5:

  ```
! + tab
  ```


- Hoja de estilos en el head del documento (la voy a llamar *css/style.css*):
    ```
  link + tab
    ```
- Creamos la estructura principal del body:
    ```
header+aside+main+footer
    ```

- Creamos el contenido del header. Observa que utilizo ya clases que utilizaré luego para hacer estilos. Es la forma más reusable y aporta cierta semántica que nos ayudará a la hora de hacer el diseño. ¡No te olvides de rellenar los menús y la fuente para el logo (*img/logo.png*)!

    ```
img+h1.title{Mis cervezas}+p.subtitle{Aficiones y locuras de un amante de la cerveza}+nav>ul.menu>li.menuitem*3>a.menulink
    ```
- Creamos el contenido del aside:
    ```
    div*2>(h1.bannerTitle+div.bannerBody>p*2>lorem) 
    ```
- Creamos el contenido del footer:
    ```
p.copyright{Sitio web realizado por un amante de la cerveza}
    ```

- Si todo está correcto, es el momento de copiar el contenido de nuestro fichero al resto de ficheros del sitio web. 

- Pulsa *CTRL + MAYS + H* para formatear el código desde Sublime Text

### index.html
- Nos ocupamos del main:

<article>
  <header>
    <h1><a href="" title=""><!-- titulo noticia --></a></h1>
    <p>fecha</p>  
  </header>
  <img src="" alt="" />
  <p></p>
</article>

Páginas 2:
Una lista de cervezas, mediante emmet

Página 3:
Formulario de contacto

Convertir el json:

- Borramos todas las llaves y paréntesis: linea 1 y seleccionamos por columna (botón derecho y mays)
Reemplazar la " por nada en current file (CTRL + MAYS + f)

- Cambiamos el ajuste de línea en Preferences->Settings user: "word_wrap": true,

- Vamos a quitar ahora las ",":
CTRL + A para seleccionar todo el texto
CTRL + MAYS + L para ir al final, pulsamos en -> para dejar de seleccionar todo y luego borramos caracter anterior (escape para quitar multicursor)
Y luego quitamos resto de caracteres.

Cada cerveza va a ser un article (seleccionamos varias con el CTRL pulsado) y luego CTRL+ALT+G para emmet
