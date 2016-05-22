# ¿Qué funciona en la Web?


## Formatos para la web (I)
- [Utilizaremos formato WebM y mp4](https://developer.mozilla.org/es/docs/HTML/Formatos_admitidos_de_audio_y_video_en_html5)
- El formato WebM se basa en una versión restringida del formato contenedor Matroska. Siempre utiliza el códec de vídeo VP8 y el códec de audio Vorbis.
- Ogg en principio podría ser prescindible. WebM da mejor relación calidad-compresión.

~~~
VIDEO CODEC SUPPORT IN SHIPPING BROWSERS
CODECS/CONTAINER	IE	FIREFOX	SAFARI	CHROME	OPERA	IPHONE	ANDROID
Theora+Vorbis+Ogg	·	3.5+	†	5.0+	10.5+	·	·
H.264+AAC+MP4	       9.0+	·	3.0+	5.0+‡	·	3.0+	2.0+
WebM	               9.0+*	4.0+	†	6.0+	10.6+	·	2.3+
* Internet Explorer 9 will only support WebM “when the user has installed
 a VP8 codec”.
† Safari will play anything that QuickTime can play. QuickTime comes 
pre-installed with H.264/AAC/MP4 support. 
There are installable third-party plugins that add support for Theora and 
WebM, but each user needs to install these plugins before Safari will 
recognize those video formats.
‡ Google Chrome promised to drop support for H.264 in 2011, but it 
never happened.
~~~

## Formatos para la web (II)
- [MP4](http://caniuse.com/#feat=mpeg4): Principalmente para IE y Safari 
- [WebM](http://caniuse.com/#feat=webm): Opera, Firefox y Google Chrome
- [Ogg](http://caniuse.com/#feat=ogv): Opera, Firefox y Google Chrome
- [Situación actual](http://www.longtailvideo.com/html5/)

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



