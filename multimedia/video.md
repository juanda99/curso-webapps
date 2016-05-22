
# Video en html5

## Un poco de historia (I)
- Antes de html5 no había ningún estándar para el video.
- Se recurría a plugins como QuickTime, RealPlayer o Flash.
- Ahora es tan sencillo como añadir la etiqueta **video**:

~~~
<video src="video.webm" controls>
</video>
~~~

- El navegador mostrará los controles básicos para reproducir o pausar el video.

## Etiqueta video
- Desgraciadamente la etiqueta **video** no funciona en todos los navegadores:

~~~
IE	FIREFOX	SAFARI	CHROME	OPERA	IPHONE	ANDROID
9.0+	3.5+	3.0+	3.0+	10.5+	1.0+	2.0+
~~~

## Inserción de video (I)
- Se pueden indicar varios sources por si el navegador no es capaz de reproducir uno de ellos
- El navegador lo intentará con el primero, luego con el segundo....

~~~
<!DOCTYPE HTML>
<html>
<body>

<video width="320" height="240" controls="controls">
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
  <source src="movie.webm" type="video/webm">
Your browser does not support the video tag.
</video>

</body>
</html>
~~~


## Inserción de video (II)

- Si indicamos el type en el video mejoraremos el rendimiento ya que el navegador sabe si puede reproducir ese video o no sin tener que intentarlo:

~~~
<source lang="html4strict">
<video controls>
  <source src="devstories.webm" 
          type='video/webm;codecs="vp8, vorbis"'/>
  <source src="devstories.mp4"
          type='video/mp4;codecs="avc1.42E01E, mp4a.40.2"'/>
</video>
</source>
~~~


## Video containers
- Muchas veces pensamos en un fichero .avi o .mp4 como si fuera un video, pero realmente es un **formato contenedor**.
- Un fichero contenedor es como un fichero .zip y en el caso del video contiene un stream de video y otro de audio.
- El fichero contenedor define como almacenar los streams de audio y video en un solo fichero.
- Aunque no es tan fácil: No todos los streams de video son compatibles con todos los ficheros contenedores. 


## Video Codecs
- Los streams de video y audio se codifican y se almacenan en un container.
- A la hora de reproducirlos, primero el reproductor debe interpretar el formato del container y luego decodificar el video y el audio
- Cuando hablamos de un codec de video nos referimos tanto un algoritmo de COdificación como al de DECodificación
- Los codec de video más populares son H264, Theora y VP8.

### H264
- También se conoce como MPEG-4 Advanced Video Coding.
- Tiene diferentes perfiles de codificación en función de la calidad del video final generado: Baseline, Main y High profiles
- El H264 está embebido en los containers más populares como mp4 y mkv.
- Tiene licencia: si codificas algo en mp4 y lo compartes con el mundo, pueden exigirte royalties.

### THEORA
- Sin ningún tipo de patentes
- En cualquier container, normalmente en ficheros .ogg

### VP8
- Comprado por Google y liberada la patente.




