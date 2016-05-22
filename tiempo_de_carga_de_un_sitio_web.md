# Tiempo de carga de un sitio web

* El tiempo de carga y la performance de una página web es muy importante para la experiencia de usuario (UX). 
* Si tu web es lenta, no solo pierdes visitas, sino potenciales clientes.
* Buscadores como Google tienen en cuanta la velocidad de carga de las webs para sus ranking de búsqueda.
* ¡Cada milisegundo es importante! Así que vamos a ver los factores que intervienen en el tiempo de carga de un sitio web:

## Latencia
* Elige un servidor adecuado comprobando la respuesta a comandos como ping o httping.
* [El tiempo de latencia influye y mucho en el load time de la página](http://www.igvita.com/2012/07/19/latency-the-new-web-performance-bottleneck/)
* Busca un hosting en Europa, no necesariamente España, pero evita "saltar el charco".
* Usa ingeniería inversa. Averigua el [http://www.maxmind.com/en/geolocation_landing proveedor de hosting de la competencia].
* El buscador bing mediante el comando ip: xx.xx.xx.xx da información sobre virtual hosting. También puedes usar webs del tipo domaintools.com (de pago).

## Minimizar los HTTP Request
* Se cumple la [regla del 80/20](http://es.wikipedia.org/wiki/Principio_de_Pareto )
* Según los estudios realizados por Yahoo! el tiempo de carga de una página media depende en un 80% de la parte del cliente y en un 20% de la parte del servidor. Los navegadores de los usuarios dedican la mayor parte del tiempo a descargar imágenes, archivos JavaScript, hojas de estilos CSS y otros recursos externos.
* Por este motivo, las mejoras en la parte del cliente generan muchos más beneficios que las mejoras en la parte del servidor.

## Imágenes
* Uso de sprites para imágenes o codificarlas inline (en base64) si las imágenes son pequeñas.
* Elección del peso adecuado de las imágenes:
  - Optimizar imágenes: Eliminación de la información innecesaria:
    - [Mediante PageSpeed Insight de Google](https://developers.google.com/speed/pagespeed/insights/) 
    - Mediante trimage
  - ¿Reducir calidad de las imágenes? 
* Se debe proporcionar la anchura y altura para que el navegador evitar renderizaciones innecesarias.
* Podemos usar programas como [Shrink O’Matic](http://toki-woki.net/p/Shrink-O-Matic/) o [ImageMagick](http://www.imagemagick.org/) para generar distintas versiones de nuestras imágenes.

* Elige el formato correcto de las imágenes: JPG para imágenes grandes y llenas de colores. GIF y PNG para el resto. [Más información](http://www.websiteoptimization.com/speed/tweak/format/ )

* Haz de la optimización de las imágenes un hábito (no solo por lo anterior: SEO, accesibilidad...)

* Uso de imágenes embebidas (eliminamos peticiones http pero deben ser imágenes pequeñas), [http://en.wikipedia.org/wiki/Data_URI_scheme puedes ver pros y contras].
* [http://www.motobit.com/util/base64-decoder-encoder.asp Herramientas de codificación].
  * Ejemplo en código html:

  ```
  <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACNbyblAAAAHElEQVQI12P4//8/w38GIAXDIBKE0DHxgljNBAAO9TXL0Y4OHwAAAABJRU5ErkJggg==" alt="Red dot">
  ```
     * Ejemplo en código css:

  ```
  div.menu {
      background-image: url('elephant.png');
      background-image:  url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQAQMAAAAlPW0iAAAABlBMVEUAAAD///+l2Z/dAAAAM0lEQVR4nGP4/5/h/1+G/58ZDrAz3D/McH8yw83NDDeNGe4Ug9C9zwz3gVLMDA/A6P9/AFGGFyjOXZtQAAAAAElFTk
                           SuQmCC');
}
```


## Uso de CDN
* Es importante la proximidad del servidor web al usuario
* Un CDN propio es una solución cara. Necesitamos clientes globales para que tenga sentido.
* Con clientes locales será importante escoger un servidor web con un buen tiempo de respuesta: pocos saltos de red, cercano.
* Un CDN es sencillo de implementar, pero si nuestra aplicación tiene escrituras a BBDD, el diseño de la arquitectura distribuida puede ser muy complejo.

## Cabeceras HTTP y cache
* Los clientes web almacenan en una caché las páginas que van visitando, sus imagenes, css, etc.
* Los servidores web indican el tiempo que tiene que estar almacenado en la cache mediante alguna de las siguientes cabeceras:
** Last Modified
* *ETag
** Expires
** Max-Age

* [Más información sobre cada uno de los métodos](http://betterexplained.com/articles/how-to-optimize-your-site-with-http-caching/ )
* [Configurar apache mediante expires](http://cjohansen.no/en/apache/using_a_far_future_expires_header)

## Uso de gzip
* Desde HTTP/1.1 los navegadores pueden indicar en las cabeceras http los formatos de compresión que soportan:
<pre>Accept-Encoding: gzip, deflate</pre>
* El servidor web lee dicho header y en función de su configuración, mandará comprimida la página web, indicándolo también en los http headers:
<pre> Content-Encoding: gzip</pre>
</div>
<div class="slide">
* Normalmente el servidor web utiliza una política de comprimir ficheros en un función de su extensión. 
* Comprimiremos html. También podemos comprimir css, js, xml o json. Las imágenes y pdf's no se comprimen.
* La compresión de los ficheros suele ser de un 70%. 
* [Más información](http://betterexplained.com/articles/how-to-optimize-your-site-with-gzip-compression/ )
* [Cómo configurar Apache para que mande las páginas comprimidas](http://www.pontikis.net/blog/speed-up-your-website-with-gzip-compression)

## Hojas de estilos
* Los css siempre en el head y antes de cualquier javascript
* Las páginas web se deben renderizar de forma progresiva: sirven al usuario para darle un indicador de progreso de carga.
* Muchos navegadores no renderizan las páginas hasta que no leen todos los css:
  * Así se evitan las penalizaciones en tiempo de ejecutar varios render
  * El usuario mientras tanto ve una página en blanco.
* Evitar el uso de @import en css ya que bloquean el renderizado 

## JavaScript
* La especificación HTTP/1.1 sugiere que los navegadores no deben descargar más de 2 ficheros de un mismo host de forma simultánea. 
* Cuando las descargas son scripts, se hacen de una en una
* ¡No siempre se pueden llevar a la parte inferior!

## Utilizar JavaScript y CSS externos
* Si los CSS o JavaScript se utilizan en varias páginas mejor externos
* El html ocupará menos y los otros ficheros estarán cacheados entre páginas de la web y no consumirán un http request
* Es negativo para visitantes de una sola página.
* El mantenimiento es más sencillo, así como la reusabilidad del código.


## Reducir peticiones DNS
* Si utilizamos varios hosts, permitimos descargas simultáneas
* Si utilizamos varios hosts podemos provocar penalizaciones por búsqueda en dns
* Los sistemas operativos y los navegadores realizan caches de dns


## Uso de versiones minified de JavaScript, CSS y html
- Para mantener la versión de desarrollo y la de producción de nuestro código sin gran complejidad lo mejor es utilizar alguna herramienta de automatización tipo **Grunt** o **Gulp**.

## Cómo verificar la carga de un sitio web
* Yslow (extensión para Google Chrome)
* Page Speed (de Google)
* [Tests desde distintas localizaciones](http://www.webpagetest.org/)
* Chrome Developer Tools o Firebug.

