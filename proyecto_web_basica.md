# Proyecto Web básica


## Pasos previos
De aquí en adelante utilizaremos emmet para producir de forma rápida el código html del sitio y git/GitHub para el control de versiones. Toda la solución que propongo está pensado para trabajar con el editor de código Sublime Text y con el plugin de Emmet instalado.

- Realizamos un fork del repositorio del ejercicio (desde GitHub)
- Realizamos un clone de nuestro fork y lo editamos mediante Sublime Text:
  ```
  cd
  git clone <url>
  cd proyecto_web_basica
  subl .
  ```

## Generación del código html del sitio


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
- Sería un buen momento para tener nuestra primera instantánea de nuestro trabajo:
  
  ```
  git status
  git add -A
  git commit -m "Generada estructura y código base"
  git puh
  ```

### index.html

- Copiamos el código del fichero *noticias.txt* en el main del documento.
- Queremos que el código quede similar a lo siguiente:

```
    <main>
        <article>
            <header>
                <h1 class="newstitle"><a href="">Como se tira la cerveza</a></h1>
                <p class="newsdate">17 de Mayo de 2016</p>
            </header>
            <p>Quienes más saben de esto recomiendan la tirada especial o en dos tiempos.</p>
            <p>El primer tiempo consiste en llenar tres cuartas partes de la copa sin generar espuma. El líquido debe caer sobre las paredes, sin movimientos de arriba y abajo de la copa y sin introducir el vaso en el grifo. Tras ponerlo en vertical, el segundo paso consiste en llenar los últimos tres centímetros de copa de una crema de espuma.</p>
            <p>Los expertos consideran que algunas modas, como las de congelar los vasos, "mata" la cerveza.</p>
        </article>
        <article>
            <header>
                <h1 class="newstitle"><a href="">El consumo moderado de cerveza tiene un efecto preventivo sobre la diabetes</a></h1>
                <p class="newsdate">14 de Mayo de 2016</p>
            </header>
            <p>El informe fue presentado por el centro Cerveza y Salud con la colaboración de la Associació de Diabètics de Catalunya y la Federación de Diabéticos Españoles.</p>
            <p>Varios componentes de la cerveza: la fibra soluble, los compuestos polifenólicos, los minerales y la baja graduación alcohólica, ayudan en el control de la diabetes. Además, la cerveza es capaz de aumentar la capacidad antioxidante del plasma.</p>
        </article>
    </main>
```

- Lo más práctico para conseguir lo anterior es hacer selecciones múltiples y "envolver" el texto con tags (pulsando CTRL+ALT+G)
- Una vez lo tengamos terminado, a guardar nuestra versión del doc:
```
git status
git add <ruta/index.html>
git commit -m "rellenado código del main"
git push
```


### cervezas.html
Es una tarea similar al caso anterior, sin embargo lo primero que debemos hacer es dejar nuestro fichero json como un texto plano que será lo que envolveremos luego en nuestras tags html.

Aquí enumero unas indicaciones para hacerlo (hay muchas formas)

- Ajuste de línea en Sublime Text:
  ```
  Menú Preferences->Settings user, insertar campo en el json: 
    "word_wrap": true
  ```

  - Obtener multicursor a principio de todas las línas: seleccionando por columna (botón derecho y mayúsculas).
- Utilizar multicursor al final de todas las líneas:
    - *CTRL + A* para seleccionar todo el texto
    - *CTRL + MAYS + L* para ir al final
    - Pulsamos en cursor para dejar de seleccionar todo
   
- Reemplazar texto: *CTRL + MAYS + f*

- Y ahora a guardar las modificaciones en GitHub...

### contacto.html




## Comportamiento responsivo
- No podemos trabajar con containers de tamaño fijo a no ser que haya unas media queries previas: la anchura de la página web la debe marcar las características del navegador cliente:
```
 <meta name="viewport" content="width=device-width, initial-scale=1">
 ```
 La etiqueta anterior la tendríamos por defecto si hubieramos escogido como plantilla base la proporcionada por el [htmlboilerplate](https://html5boilerplate.com/). Lo más rápido sería mediante un [plugin de Sublime](https://packagecontrol.io/packages/HTML%20Boilerplate).
 
 

