# Imágenes



## Introducción
- Las imágenes un elemento clave para una web bien diseñada
- [ Las páginas web atractivas se encuentran, no se hacen](http://www.sitebuilderreport.com/blog/where-the-best-designers-go-to-find-photos-and-graphics):
    - Búsqueda de imágenes
    - Búsqueda de iconos
    - Búsqueda de patterns


## Logotipos, imágenes y diseño
- El diseño es clave para una web
- ¿Dónde encontrar buenos diseñadores?
- ¿Dónde darse a conocer como diseñador? 
    - [Dribble](http://dribbble.com/) 
    - [Behance](http://www.behance.net/): portfolios online de diseñadores en la nube de Adobe.
- [The awards for design, creativity and innovation on the Internet](http://www.awwwards.com/) 


## Bancos de fotografías
- Algunos clásicos y más caros, por ejemplo [Corbis](http://www.corbisimages.com/)
- Otros, los llamados microstocks más amateur pero con precios más reducidos:
    - <http://www.shutterstock.com/>
    - <http://www.istockphoto.com/>
    - <http://www.fotolia.com>
    - <http://www.bigstockphoto.com/>
    - <http://www.sxc.hu/> (gratuito)


## Caso práctico
- La elección de imágenes puede llevar mucho tiempo y es vital para el aspecto final de nuestra web.
- Ejemplos de imágenes para webs de accidentes de tráfico:
    - [http://www.solernaharro.com/](http://www.solernaharro.com/)
    - [http://abogadoaccidentetrafico.es/](http://abogadoaccidentetrafico.es/)
    - [http://www.marianosanchez.com/](http://www.marianosanchez.com/)
- ¿Qué tipo de imágenes utilizarías tu?
- El enfoque del cliente es importante para el desarrollo de la web


## Optimización de imágenes
- Podemos utilizar PageSpeed de Google
- Podemos instalar algún software como [trimage](http://trimage.org/):

```
sudo apt-get install trimage
```


## Retocar imágenes
- En ocasiones es bueno retocar las imágenes:
    - Brillo, contraste, reducción de ruido
    - Recortar la imagen para centrar la atención en una parte de ella.
    - Alinear horizonte, ojos rojos....
- Utilizaremos programas como photoshop o gimp.


## Tipos de imágenes
- **Imágenes de mapa de bits**:
    - Están formadas por un conjunto de puntos (píxeles) contenidos en una tabla. 
    - Cada uno de estos puntos tiene un valor o más que describe su color.
    - Se modifican mediante Gimp o Photoshop
- **Imágenes vectoriales**:
    - Representaciones de entidades geométricas tales como círculos, rectángulos o segmentos. 
    - Están representadas por fórmulas matemáticas (un rectángulo está definido por dos puntos; un círculo, por un centro y un radio...)
    - Se modifican mediante Inkscape o CorelDraw


## ¿Qué tipo de imágenes utilizamos?

- Las imágenes de mapas de bits se pixelan.
- Las imágenes vectoriales son más simples, aunque la superposición de formas simples pueden producir resultados impresionantes.
- Las fotografías serán siempre mapas de bits
- Las imágenes vectoriales se introducen en html5 por medio del formato svg (hasta ahora mediante Flash).
- Interacccionar entre imágenes vectoriales y JS es sencillo.


## Imágenes en dispositivos
- Útil para dar un aspecto más moderno y tecnológico
- Muy usado en programas de software, mostrando por ejemplo una aplicación dentro de un ipad
- Desde Ubuntu podremos capturar la pantalla o ventana actual
- Hay varios servicios que nos generan nuestra imagen en un dispositivo físico:
    - <http://placeit.breezi.com> 
    - <http://mockuphone.com>
    - <http://developer.android.com/distribute/promote/device-art.html>
    - <http://aarnis.com/demo.html>
    - <http://goo.gl/aLuT6e> 


## Tratamiento de imágenes desde consola (I)
- Instalaremos el [http://www.imagemagick.org/ paquete imagemagick] para tratar las imágenes:

```
apt-get install imagemagick
```

- Cambiar formato de una imagen:
```
$ convert rose.jpg rose.png
```

- Especificar el nivel de compresión para imágenes jpg (de 0 a 100, por defecto 92):

```
convert howtogeek.png -quality 95 howtogeek.jpg
```

- Cambiar el tamaño de las imágenes:
    - En este caso se sobreescribe la imagen original
    - La imagen intentará guardar la proporción

```
convert example.png -resize 200x100 example.png
```

- En este caso la imagen no guardará la proporción (por la exclamación):

```
convert example.png -resize 200x100! example.png
```

- Ancho 200, el alto según proporciones de la imagen:

```
convert example.png -resize 200 example.png
```

- Alto 100, ancho según proporciones de la imagen:
```
convert example.png -resize x100 example.png
```

- Procesos en batch:
    - En este caso rotamos todas las imágenes de tipo png del directorio actual 90º y las guardamos con el prefijo "rotated"

```
for file in *.png; do convert $file -rotate 90 rotated-$file; done
```

- También podremos realizar efectos como marcas de agua...
- Para más información, ejecutamos "man convert"



