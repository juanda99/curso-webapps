# Audio



## Voces de Audio
- Pueden ser caras:
    - 250 euros por 5 minutos de voz. 
    - El equipo de audio no lo pones tu :-)
    - <http://www.voices.com/> Elegir una voz
    - ¿Te suena?
{%youtube%}07wVo1hnmdQ{%endyoutube%}


## Audio Codecs
- Como los codecs de video existen con o sin pérdida
- Como en los de video, para la web nos interesan los que tienen perdida (pero a su vez menor peso)
- Nos centraremos en los codecs generales (hay específicos por ejemplo para telefonía).
- Al descodificar el audio mandamos los datos del stream de audio a los altavoces


- Los audios tienen canales (los videos no): cada altavoz se alimenta de un channel del stream de audio.
- Los codecs de propósito general codifican normalmente 2 canales.
- En la web se utilizan exlusivamente tres codecs: MP3, AAC y Vorbis.


### MP3
- Formalmente llamado MPEG-1 Audio Layer 3
- Hasta 2 canales de sonido
- Distintos bitrates 64kbps, 128kbps, 192kbps 
- A mayor bitrate el fichero será más pesado y tendrá más calidad de audio


- El bitrate y la calidad de audio no tienen una relación lineal: 
    - 128kbps se oye con más del doble de calidad que 64kbps
    - 256k no se oye con el doble de calidad que 128kbps
- Podemos codificar con un bitrate constante o variable (por ej. codificando a un bitrate bajo los silencios de audio).
- Tiene patentes, por eso Linux no lo reproduce por defecto.


### AAC
- Formalmente llamado Advanced Audio Coding
- Hasta 64 canales de sonido
- Estandarizado por Apple en 1997. Lo utilizo como formato por defecto para su iTunes Store.
- Diseñado para dar mayor calidad de audio que MP3 al mismo bitrate
- Sin límite de bitrate (MP3 lo tiene en 320kbps)
- La librería libre para codificar en AAC se llama FAAC.
- Usa profiles, de forma similar a MP4.


### VORBIS
- Denominado a veces OGG-VORBIS pero OGG es el container
- Suele ir embebido en ficheros ogg o webm pero también puede ir en mp4, mkv 
- Soporta un gran número de canales de sonido



