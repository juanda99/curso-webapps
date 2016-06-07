# Tiempo de carga de un sitio web


## Latencia
- Elige un servidor adecuado comprobando la respuesta a comandos como ping o httping.
- [El tiempo de latencia influye y mucho en el load time de la página](http://www.igvita.com/2012/07/19/latency-the-new-web-performance-bottleneck/) 
- Busca un hosting en Europa, no necesariamente España, pero evita "saltar el charco".
- Usa ingeniería inversa. Averigua el [proveedor de hosting de la competencia](http://www.maxmind.com/en/geolocation_landing)
- El buscador bing mediante el comando ip: xx.xx.xx.xx da información sobre virtual hosting. También puedes usar webs del tipo domaintools.com (de pago).


- El tiempo de carga y la performance de una página web es muy importante para la experiencia de usuario (UX). 
- Si tu web es lenta, no solo pierdes visitas, sino potenciales clientes.
- Buscadores como Google tienen en cuanta la velocidad de carga de las webs para sus ranking de búsqueda.
- ¡Cada milisegundo es importante!


## Minimizar los HTTP Request
- Se cumple la [regla del 80/20 o Principio de Pareto](http://es.wikipedia.org/wiki/Principio_de_Pareto) 
- Según los estudios realizados por Yahoo! el tiempo de carga de una página media depende en un 80% de la parte del cliente y en un 20% de la parte del servidor. Los navegadores de los usuarios dedican la mayor parte del tiempo a descargar imágenes, archivos JavaScript, hojas de estilos CSS y otros recursos externos.
- Por este motivo, las mejoras en la parte del cliente generan muchos más beneficios que las mejoras en la parte del servidor.


### Imágenes
- Uso de sprites (y también image maps para imágenes contiguas). 
- Elección del tamaño adecuado de las imágenes: el html no debe escalar la imagen.
- PageSpeed Insights (by Google) directamente da las imágenes optimizadas y también información sobre el tamaño para escalarla (ojo, habrá que correr PageSpeed con UserAgents diferentes si la web es responsiva).
- Podemos usar programas como [Shrink O’Matic](http://toki-woki.net/p/Shrink-O-Matic/) o [ImageMagick](http://www.imagemagick.org/) para generar distintas versiones de nuestras imágenes.


#### Haza de la optimización de las imágenes un hábito
- Uso de atributos: texto alternativo (alt), título de la imagen (title) y width y height.
- [Elige el formato correcto de las imágenes](http://www.websiteoptimization.com/speed/tweak/format/): JPG para imágenes grandes y llenas de colores. GIF y PNG para el resto.
- Nombres de ficheros de imágenes descriptivos (SEO) y en la medida de lo posible con links (al usuario le gustan y a google también).


- Uso de imágenes embebidas:
  - Eliminamos peticiones http
  - Deben ser imágenes pequeñas, [puedes ver pros y contras](http://en.wikipedia.org/wiki/Data_URI_scheme).
  - [Herramientas de codificación](http://www.motobit.com/util/base64-decoder-encoder.asp). Ejemplo en código:

```
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACNbyblAAAAHElEQVQI12P4//8/w38GIAXDIBKE0DHxgljNBAAO9TXL0Y4OHwAAAABJRU5ErkJggg==" alt="Red dot">
```

```
div.menu {
    background-image: url('elephant.png');
    background-image:  url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQAQMAAAAlPW0iAAAABlBMVEUAAAD///+l2Z/dAAAAM0lEQVR4nGP4/5/h/1+G/58ZDrAz3D/McH8yw83NDDeNGe4Ug9C9zwz3gVLMDA/A6P9/AFGGFyjOXZtQAAAAAElFTk
                           SuQmCC');
}
```


## Uso de CDN
- Es importante la proximidad del servidor web al usuario
- Un CDN propio es una solución cara. Necesitamos clientes globales para que tenga sentido.
- Con clientes locales será importante escoger un servidor web con un buen tiempo de respuesta: pocos saltos de red, cercano.
- Un CDN es sencillo de implementar, pero si nuestra aplicación tiene escrituras a BBDD, el diseño de la arquitectura distribuida puede ser muy complejo.


## Cabeceras HTTP y cache
- Los clientes web almacenan en una caché las páginas que van visitando, sus imagenes, css, etc.
- Los servidores web indican el tiempo que tiene que estar almacenado en la cache mediante alguna de las siguientes cabeceras:
  - Last Modified
  - ETag
  - Expires
  - Max-Age

- [Más información sobre cada uno de los métodos](http://betterexplained.com/articles/how-to-optimize-your-site-with-http-caching/)
- [Configurar apache mediante expires](http://cjohansen.no/en/apache/using_a_far_future_expires_header)


## Uso de gzip
- Desde HTTP/1.1 los navegadores pueden indicar en las cabeceras http los formatos de compresión que soportan:
<pre>Accept-Encoding: gzip, deflate</pre>
- El servidor web lee dicho header y en función de su configuración, mandará comprimida la página web, indicándolo también en los http headers:
<pre> Content-Encoding: gzip</pre>


- Normalmente el servidor web utiliza una política de comprimir ficheros en un función de su extensión. 
- Comprimiremos html. También podemos comprimir css, js, xml o json. Las imágenes y pdf's no se comprimen.
- La compresión de los ficheros suele ser de un 70%. 
- Más información](http://betterexplained.com/articles/how-to-optimize-your-site-with-gzip-compression/)
- [Cómo configurar Apache para que mande las páginas comprimidas](http://www.pontikis.net/blog/speed-up-your-website-with-gzip-compression)


## Colocación de hojas de estilos en la parte superior
- Las páginas web se deben renderizar de forma progresiva: sirven al usuario para darle un indicador de progreso de carga.
- Muchos navegadores no renderizan las páginas hasta que no leen todos los css:
  - Así se evitan las penalizaciones en tiempo de ejecutar varios render
  - El usuario mientras tanto ve una página en blanco.
  - Mejor no utilizar @import en los CSS porque provocan bloqueos.

- Resumiendo... **los css siempre en el head y antes de cualquier javascript**


## Colocación de scripts en la parte inferior
- La especificación HTTP/1.1 sugiere que los navegadores no deben descargar más de 2 ficheros de un mismo host de forma simultánea. 
- Cuando las descargas son scripts, se hacen de una en una
- ¡No siempre se pueden llevar a la parte inferior!


## Utilizar JavaScript y CSS externos
- Si los CSS o JavaScript se utilizan en varias páginas mejor externos
- El html ocupará menos y los otros ficheros estarán cacheados entre páginas de la web y no consumirán un http request
- Es negativo para visitantes de una sola página.
- El mantenimiento es más sencillo, así como la reusabilidad del código.


## Reducir peticiones DNS
- Si utilizamos varios hosts, permitimos descargas simultáneas
- Si utilizamos varios hosts podemos provocar penalizaciones por búsqueda en dns
- Los sistemas operativos y los navegadores realizan caches de dns


## Uso de versiones minified de JavaScript y CSS
- Obliga a tener dos versiones, desarrollo y producción
- Automatizaremos la generación de la versión de producción:
   - Es lo que se conoce como build o compilación
   - Usaremos herramientas tipo gulp o grunt



## Verificar la carga de una página
- Utilizando Chrome developer tools podemos ver lo que tarda en **empezar a pintar** o la pestaña de Network
- Buena documentación de Yahoo en su [portal Yslow](http://yslow.es/) (extensión para Google Chrome)
- [PageSpeed Insights (de Google)](https://developers.google.com/speed/pagespeed/insights/)
- [Tests desde distintas localizaciones](http://www.webpagetest.org/) 




