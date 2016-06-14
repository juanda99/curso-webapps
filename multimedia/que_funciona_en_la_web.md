# ¿Qué funciona en la Web?


## Formatos para la web
- En el 2010 por temas de compatibilidad era necesario usar más de un formato
  - [MP4](http://caniuse.com/#feat=mpeg4): Principalmente para IE y Safari 
  - [WebM](http://caniuse.com/#feat=webm): Opera, Firefox y Google Chrome
  - [Ogg](http://caniuse.com/#feat=ogv): Opera, Firefox y Google Chrome
- El formato WebM se basa en una versión restringida del formato contenedor Matroska. Siempre utiliza el códec de vídeo VP8 y el códec de audio Vorbis.
- Ogg en principio podía ser prescindible. WebM da mejor relación calidad-compresión.

- Actualmente con usar mp4 es suficiente.


## Configuración servidor web
- El servidor web tiene que tener los mime types configurados para la reproducción de videos en los navegadodores
- Será lo que envíe en el header como content-type y que el navegador puede requerir.
- En el servidor web Apache lo haremos en el fichero .htaccess o en el httpd.conf/apache2.conf:
~~~
AddType video/ogg .ogv
AddType video/mp4 .mp4
AddType video/webm .webm
~~~


## Codificación de Vídeo
- ¿livav o ffmpeg? [Ver resumen de problemática](http://blog.pkh.me/p/13-the-ffmpeg-libav-situation.html)
- Por defecto Ubuntu funciona con livav. 
- [Instalación de ffmpeg](https://ffmpeg.org/trac/ffmpeg/wiki/UbuntuCompilationGuide)
- [Codificación con H.264](https://www.virag.si/2012/01/web-video-encoding-tutorial-with-ffmpeg-0-9/) 
- [Codificación con WebM y Ogg](https://www.virag.si/2012/01/webm-web-video-encoding-tutorial-with-ffmpeg-0-9/) 
- Otra opción para codificar mp4: <http://handbrake.fr/>
- Otra opción para codificar Ogg-Vorbis: <http://v2v.cc/~j/ffmpeg2theora/>


## Videos responsivos

### css habitual
- Declarar dimensiones "estáticas" no es buena idea: 

~~~
<video width="400" height="300" ....
~~~

- Utilizaremos porcentajes: el vídeo se adaptará a su elemento contendedor.
- En html5 es bueno definir solo la anchura para que el vídeo mantenga su proporción:

~~~
<video width="100%" ....
~~~

- Mediante css:

~~~
video {
  width: 100%    !important;
  height: auto   !important;
}
~~~


### Vídeos de youtube, vimeo mediante iframe

- Código inserción vídeos youtube:

~~~
<iframe width="640" height="480" 
src="http://www.youtube.com/embed/oDlsOyPKUTM" 
frameborder="0" allowfullscreen>
</iframe>
~~~

- Código inserción vídeos vimeo:

~~~
<iframe src="http://player.vimeo.com/video/57444237" width="500" 
height="281" frameborder="0" webkitAllowFullScreen 
mozallowfullscreen allowFullScreen>
</iframe> 
~~~

### Vídeos de youtube, vimeo mediante object

- También se puede usar object y embed para insertar código no html. Por ejemplo youtube con Flash:

~~~
<object width="640" height="480">
   <param name="movie" value="http://www.youtube.com/v/
	oDlsOyPKUTM?hl=es_ES&amp;version=3"></param>
   <param name="allowFullScreen" value="true"></param>
   <param name="allowscriptaccess" value="always"></param>
   <embed src="http://www.youtube.com/v/oDlsOyPKUTM?hl=es_ES&amp;version=3" 
		type="application/x-shockwave-flash" 
      width="640" height="480" allowscriptaccess="always" allowfullscreen="true">
   </embed>
</object>
~~~

- En desuso

### Vídeo responsivo por iframe
- Si no se especifica las dimensiones de un elemento tipo iframe, embed, object y canvas, en navegador lo dimensiona como 300x150px
- No se puede utilizar el truco de 100% width, el navegador pondría una altura de 150px que sería normalmente demasiado pequeña.
    - Ver solución: <http://css-tricks.com/NetMag/FluidWidthVideo/Article-FluidWidthVideo.php> 



