# PhoneGap



## Introducción
- Vamos a crear una pequeña práctica con la que aprenderemos las características básicas de Cordova, manejar la API de para usar las características nativas del dispositivo y a crear una aplicación con una arquitectura óptima para móviles.

- Echa un [vistazo primero al diseño y  arquitectura de una aplicación en PhoneGap](http://media.formandome.es/phonegap/presentacion/phonegap_intro.html). Ahí entre otras cosas aclaro las diferencias entre PhoneGap y Cordova.



## Requisitos previos

- En el capítulo de *Entorno de trabajo* vimos como instalar Android Studio junto con el JDK
- Desde el software de Android Studio podemos instalar los SDK de Android que necesitemos (están instalados al menos 4.3, 5 y 6) 
- Se configuraron también los PATH de la máquina necesarios. Si tu usuario es diferente, puede ser que tengas que cambiar algo.


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


## Nuevo proyecto de Cordova

- Instalamos Cordova
```
npm i -g cordova
```
- Creamos nuestro proyecto mediante el comando instalado anteriormente:
```
cd
cordova create proyecto com.tunombre.proyecto Proyecto
```

El primer parámetro es el directorio donde se guardará e proyecto. El segundo es un identificador para el proyecto con estructura de DNS inverso, el tercero es el nombre del proyecto y título que mostrará la aplicación. Puede ser útil poner el modificador -d para mostrar el progreso de creación del proyecto

- Comprobamos para que plataformas podemos generar nuestro apk:

```
$ cordova platform ls
Installed platforms:
  
Available platforms: 
  amazon-fireos ~3.6.3 (deprecated)
  android ~5.1.1
  blackberry10 ~3.8.0
  browser ~4.1.0
  firefoxos ~3.6.3
  ubuntu ~4.3.3
  webos ~3.7.0
```

- Instalamos la plataforma android (se creará un directorio bajo *platforms*):

  ```
  $ cordova platform add android
  Adding android project...
  Creating Cordova project for the Android platform:
      Path: platforms/android
      Package: com.juanda.futbolistas
      Name: Futbolistas
      Activity: MainActivity
      Android target: android-23
  Android project created with cordova-android@5.1.1
  Discovered plugin "cordova-plugin-whitelist" in config.xml. Adding it to the project
  Fetching plugin "cordova-plugin-whitelist@1" via npm
  Installing "cordova-plugin-whitelist" for android

  This plugin is only applicable for versions of cordova-android greater than 4.0. If you have a previous platform version, you do *not* need this plugin since the whitelist will be built in.
  ```          


### Plugins de Cordova
- Observa que en el paso anterior se ha instalado un plugin que estará en el directorio de plugins.
- Cordova funciona en base a plugins que le van añadiendo funcionalidad a nuestro software, así el fichero de js no crece demasiado si no es necesario.
- Puedes echar un vistazo al [directorio de plugins de Cordova](https://cordova.apache.org/plugins/) y su compatibilidad con las distintas plataformas móviles.
- Los plugins se instalan mediante:

  ```
  cordova plugin add <nombre-plugin>
  ```


### Requerimientos de software

- Podemos comprobar si cumplimos los requerimientos para el desarrollo:
```
$ cordova requirements

Requirements check results for android:
Java JDK: installed .
Android SDK: installed 
Android target: installed android-18,android-19,android-21,android-22,android-23
Gradle: installed 
```
- Necesitamos un emulador de Android. Voy a utilizar **Android Virtual Device**, pero Virtual Box no permite virtualización anidada :-(


### Evento deviceready
- Si ejecutamos el código base por defecto en un navegador, no funcionará:
  - El código principal se dispara en el **evento deviceready**, este evento marca que las APIs del dispositivo están ya cargadas y accesibles.
  - Cordova consiste en dos partes de código: nativo y JavaScript. Mientrase no se carga el código nativo, aparece la imagen de carga. 
- Si lo ejecutamos en el emulador, funcionará correctamente:
  - Lanzamos el emulador
  
    ```
    android avd &
    ```
  
  - Ejecutamos nuestro proyecto:

  ```
  cordova run android
  ```


### Añadir un plugin
- Vamos a modifica el fichero index.js para que muestre vía consola algún dato del dispositivo:
```
....
    receivedEvent: function(id) {
        var parentElement = document.getElementById(id);
        var listeningElement = parentElement.querySelector('.listening');
        var receivedElement = parentElement.querySelector('.received');

        listeningElement.setAttribute('style', 'display:none;');
        receivedElement.setAttribute('style', 'display:block;');

        console.log('Received Event: ' + id);
        console.log(device.cordova);
        console.log(device.model);
    }  
```
- Si ejecutamos nuestro proyecto de nuevo, dará un error, se pueden ver trazas mediante:

  ```
  adb logcat
  ```
- Instalamos el plugin correspondiente y lanzamos de nuevo el proyecto:

  ```
  cordova plugin add cordova-plugin-device
  cordova run android
  ```

### Compilación
- Los comandos más habituales son los siguientes:
```
cordova run android
```
  - El proyecto se ejecuta en el dispositivo físico y si no existe, en el emulador
  - Se realiza una compilación previa para poder instalarlo y ejecutarlo en el dispositivo
```
cordova emulate android
```
  - El proyecto se ejecuta en el emulador
```
cordova build android
```
  - Se genera el apk del proyecto, para poderlo instalar "a mano".


### Nuestro entorno de desarrollo
- Probaremos todo lo que podamos directamente en el navegador
- Si podemos, utilizamos emulador... aunque **VirtualBox no soporta virtualización anidada**
- Generamos el apk y lo instalamos en el movil
  - Necesitamos **habilitar sideload** (Ajustes->Seguridad->Origenes desconocidos)
  - El apk se puede enviar de forma cómoda mediante **AirDroid** o se puede colgar en una url y acceder vía navegador
  - Para instalarlo basta con hacer doble click
- Utilizaré **Screen Stream Mirroring** para compartir la pantalla

## Práctica de Cordova
- Hacemos un [fork de mi repositorio](git@github.com:juanda99/practica-cordova.git)
- Hacemos git clone del nuevo repositorio creado 
- Nos situamos dentro y creamos nuestro proyecto:
```
  cd practica-cordova
  cordova create futbolistas com.tunombre.futbolistas Futbolistas
```
- Copiamos los ficheros de nuestra práctica
  ```
  cp -r sources/ futbolistas/www/ 
  ```