# PhoneGap



## Introducción
Vamos a crear una pequeña práctica con la que aprenderemos las características básicas de Cordova, manejar la API de para usar las características nativas del dispositivo y a crear una aplicación con una arquitectura óptima para móviles.

Echa un [vistazo primero al diseño y  arquitectura de una aplicación en PhoneGap](http://media.formandome.es/phonegap/presentacion/phonegap_intro.html).


## Práctica
- Sigue el tutorial que he publicado en http://www.formandome.es/android/phonegap-cordova-tutorial/.


## Requisitos previos

- En el capítulo de *Entorno de trabajo* vimos como instalar Android Studio junto con el JDK
- Desde el software de Android Studio podemos instalar los SDK de Android que necesitemos (están instalados al menos 4.3, 5 y 6) 
- Se han configurado también en el apartado anterior, los PATH de la máquina necesarios. Si tu usuario es diferente, puede ser que tengas que cambiar algo.


## ADB
- ADB son las siglas de Android Debug Bridge
- Es una herramienta de desarrollo incluida en el SDK de Android.
- Comunica el dispositivo Android o el emulador con el ordenador.
- Sirve para instalar aplicaciones, ver ficheros de log, hacer push o pull de ficheros...
- Para ver errores utilizaremos:
``` 
adb logcat
```


## Emuladores

- Mediante *android avd* podemos definir los emuladores que necesitemos:
  - No olvides, en *Emulation options*, marcar la opción *use host GPU*

