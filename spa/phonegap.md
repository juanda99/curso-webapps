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
- Copiamos los ficheros de nuestra práctica y borramos lo que no nos interesa:

  ```
  rm futbolistas/www/css/index.css 
  rm futbolistas/www/js/index.js
  cp -r sources/* futbolistas/www/ 
  ```


### Test del código base

- Probamos el funcionamiento desde el navegador:

```
cd futbolistas/www
open index.html
```
- Podemos probar también desde el emulador:

  ```
  cordova platform add android
  cordova run android
  ```

### Método de almacenamiento
- Definimos varios métodos de almacenamiento mediante ficheros y clases independientes. 
- Todas las clases presenten la misma interfaz de modo que **utilizar uno u otro método de almacenamiento sea transparente para el desarrollo de la aplicación**.
- Tipos de almacenamiento:
  - **Almacenamiento en memoria** (fichero *js/adapters/memory-adapter.js*)
  - **Almacenamiento en remoto** (fichero *js/adapters/jsonp-adapter.js*)
  - **Almacenamiento mediante LocalStorage** (fichero *js/adapters/localstorage-adapter.js*)
  - **Almacenamiento en base de datos local** (fichero *js/adapters/websql-adapter.js*)
  - [**Descartamos indexDB** (no lo soporta PhoneGap ni iOS)](http://caniuse.com/#search=indexdb)
- Abre cada uno de los ficheros anteriores para explorar cada uno de los métodos de almacenamiento.


### Cambiar el tipo de almacenamiento

- Prueba la aplicación con cada uno de los métodos de almacenamiento anteriores
- La aplicación por defecto está configurada para trabajar con almacenamiento en memoria. Para cambiar el método de almacenamiento:
  - En el fichero *index.html*, cambia el fichero *memory-adapter.js* por el que corresponda: *jsonp-adapter.js*, *localstorage-adapter.js*, o *websql-adapter.js*.
  - En *js/app.js*, reemplaza la instanciación de MemoryAdapter con el que corresponda según el método de almacenamiento elegido: JSONPAdapter, LocalStorageAdapter, o WebSqlAdapter.
  - Prueba la aplicación


### Uso de notificación nativa
- El típico alert de JavaScript puede ser algo rígido para tu aplicación PhoneGap que aparenta ser nativa. Puede ser que queramos personalizar la ventana de aviso mediante un título, un texto específico en el botón o incluso una función de callback. La función alert de JavaScript no nos lo va a permitir.
- Para hacer una llamada a la ventana de diálogo nativa deberemos [añadir el plugin correspondiente](https://www.npmjs.com/package/cordova-plugin-dialogs):
```
cordova plugin add cordova-plugin-dialogs
```
Al utilizar nuestra aplicación algo nativo, deberemos añadir la librería cordova.js:
```
<script src="cordova.js"></script>
```

- Esta instrucción hara que Cordova inserte la versión específica de Cordova a la plataforma en la que estemos desarrollando en tiempo de compilación. Es decir, el fichero cordova.js no debería estar presente en la carpeta www de nuestro proyecto.
- Por último deberemos hacer un override de la función window.alert() cuando ejecutemos nuestra aplicación en un dispositivo que disponga del objeto navigator.notification.alert(). Añadiremos el siguiente código en nuestra aplicación (fichero *app.js*, en el bloque de registro de eventos):

```
document.addEventListener('deviceready', function () {
  if (navigator.notification) { 
  // Si disponemos de notificaciones nativas, sobreescribimos el alert del navegador:
    window.alert = function (message) {
      navigator.notification.alert(
        message,    // mensaje
        null,       // función de callback
        "Workshop", // título
        'OK'        // Nombre botón
      );
    };
  }
}, false);  
```

- Prueba a ejecutar la aplicación desde el dispositivo móvil o emulador y desde el navegador del PC. Observa que la notificación cambia en función del entorno.


## Evita el retraso de 300ms en el clic

- Si pulsas el botón de ayuda y según el dispositivo/emulador puedes notar cierto retraso hasta que aparece la ventana de diálogo.
- Esto es debido a que el navegador puede esperar en torno a 300ms por si el usuario hace un doble clic. Para evitarlo podemos utilizar alguna [librería de JavaScript como FastClick](https://github.com/ftlabs/fastclick)

- Añade el script en el fichero index.html:
```
<script src="lib/fastclick.js"></script>
```


- Registra FastClick en el fichero app.js. En la documentación de FastClick se explica como integrarlo, pero quizá lo más sencillo sea dentro de la función manejadora del evento deviceready que hemos utilizado en el paso anterior, añadiendo la siguiente instrucción:
```
FastClick.attach(document.body);
```
- Comprueba desde el emulador o movil que ha desaparecido el retraso si hubiese. En principio bajo Chrome y al tener el viewport con user-scalable=no, no sería necesario.


## Arquitectura SPA

- Vamos a configurar ahora nuestra aplicación para que se ejecute en una sola página:
  - Su funcionamiento será más fluido
  - Pretendemos que la velocidad de ejecución sea lo más parecido a ejecutar código nativo.

- En el fichero index.html borramos todo el contenido del body (salvo los scripts) ya que lo generaremos mediante JavaScript


- Definiremos una función que será la encargada de renderizar el home de nuestra aplicación, dentro de la sección de funciones locales del script app.js:
```
    function renderHomeView() {
       var html = "<header>" +
                     "<h1>Futbolistas</h1>" +
                  "</header>" +
                  "<input id='btnBuscar' type='search' placeholder='Introduce futbolista'/>" +
                  "<ul id='lstFutbolistas'></ul>"
      $('body').html(html);
      $('#btnBuscar').on('keyup', encontrarPorNombre);
    }
 ```


- Observa que hemos quitado el botón de ayuda y que el registro del evento keyup lo metemos dentro de la función renderHomeView, por lo que deberemos quitarlo de donde estaba anteriormente (sección registro de eventos). También quitaremos el manejador del botón de ayuda.

- Modificaremos la lógica de la aplicación, de modo que una vez que se inicialice el adaptador de datos se muestre la vista de la página inicial:
```
    adapter.inicializar().done(function () {
        console.log("Inicializado: Adaptador de datos");
        renderHomeView();
    });
 ```
 
 ## Elección de framework de CSS
- A la hora de mostrar nuestro html en pantalla es importante utilizar un **framework css específico de móvil**, es decir, diseñado para un renderizado rápido:

- Uso propiedades específicas de css para animaciones, que utilicen la GPU
- Evitar el uso de propiedades como box-shadow, border-radius, gradientes o text-align


- Ejemplos:
  - [Ionic](http://ionicframework.com/) que viene “preparado” para funcionar con Angularjs y que se integra perfectamente con PhoneGap 
  - [Intel App Framework](http://app-framework-software.intel.com/) que viene preparado con un css específico para cada plataforma móvil, para simular más el aspecto nativo
  - Adobe (impulsor de PhoneGap) tambień tiene el suyo: [Topcoat](v).

- Usaremos Topcoat


## Uso de templates: handlebars
- Escribir código html desde JavaScript es propenso a errores (comillas simples en vez de dobles, alternar texto con variables…) y además poco legible.

- Utilizaremos templates para desacoplar la definición de la interfaz de usuario (html) del código. Si no has usado nunca handlebars, echa un vistazo a la [documentación oficial](http://handlebarsjs.com/) (es corta) y a [un post de ejemplo de uso de handlebars](http://www.formandome.es/javascript/handlebars-ejemplo-uso/) y otro [post de precompilación de handlebars](http://www.formandome.es/javascript/handlebars-precompilacion/).

- Vamos a crear dos templates, una para la página de inicio y otra para mostrar los elementos de la lista de futbolistas, que guardaremos en la carpeta templates.

- En la página de inicio y según la documentación de topcat.io necesitaremos los siguientes elementos:
  - Navigation bar
  - Search Input
  - List
- Plantilla para la página de inicio (fichero home.handlebars):
```
<div class="topcoat-navigation-bar">
    <div class="topcoat-navigation-bar__item center full">
        <h1 class="topcoat-navigation-bar__title">Futbolistas</h1>
    </div>
</div>
<div class="search-bar">
<input type="search" value="" placeholder="buscar" class="topcoat-search-input" id="btnBuscar">
</div>
<div class="topcoat-list">
    <ul class="topcoat-list__container list" id="lstFutbolistas">
  </ul>
</div>
```
- Plantilla para la lista de futbolistas (fichero listaJugadores.handlebars):
```
  {{#.}}
    <li class="topcoat-list__item">
      <a href="#futbolistas/{{id}}">
            <img src="assets/img/{{imagen}}">
            <p>{{nombre}} {{apellido}}</p>
            <p>{{equipo}}</p>
            <span class="chevron"></span>
        </a>
      </li>
    {{/.}}
 ```
 - Precompilamos las plantillas:
 ```
 Precompilamos las plantillas:
 ```
 $ handlebars templates/ -f js/templates.js
 ```
 - Cambiamos las funciones de app.js para que carguen el template:
 ```
     function renderHomeView() {
      $('body').html(Handlebars.templates.home());
      $('#btnBuscar').on('keyup', encontrarPorNombre);
    }
    function encontrarPorNombre() {
        adapter.encontrarPorNombre($('#btnBuscar').val()).done(function (futbolistas) {
           $("#lstFutbolistas").html(Handlebars.templates.listaJugadores(futbolistas)); 
	});
    }
  ```
  
- Copiamos el framework de topcoat dentro de nuestro proyecto. Podemos elegir entre un theme claro y otro oscuro.

```
<link href="assets/topcoat/css/topcoat-mobile-light.css" rel="stylesheet">
```
- Cargamos también el script de handlebars (al precompilar, cogeremos el runtime) y los templates precompilados:

  ```
  <script src="lib/handlebars.runtime-v1.3.0.js"></script>
  <script src="js/templates.js"></script>
  ```

- Si probamos el resultado, vemos que se le puede dar un toque adicional de diseño. Debemos crear un fichero style.css que añadiremos a nuestro index.html:

  ```
  <link href="assets/css/styles.css" rel="stylesheet">
  ```
/*Situamos la caja de búsqueda dentro de un div y le damos el 100% de anchura*/
.search-bar {
    padding:10px 10px 12px 8px;
}

.search-bar > input {
    width: 100%;
}

a {
    text-decoration: none;
    color: inherit;	
    -webkit-touch-callout: none;
    -webkit-tap-highlight-color: rgba(0, 0, 0);
}

.list {
    list-style-type: none;
    border-top: none !important;
}

.list > li {
    position: relative;
    clear: both;
    padding: 0px;
    margin: 0px;
}

.list > li:nth-of-type(1) {
    border-top: none;
}

.list > li > a {
    margin: 0px;
    display: block;
    height: 57px;
    padding: 4px;
}


.list > li > a > p:nth-of-type(1) {
    margin: 8px 0px 0px 0px;
    font-weight: bold;
}

/*El nombre del juegador en negro, el equipo en gris:*/
.list > li p:nth-of-type(2) {
    margin: 0px;
    color: #777;
}

/*Las imágenes en la lista, con un ancho fijo, y el texto a su derecha:*/
.list > li img {
    width: 57px;
    height: 57px;
    float: left;
    margin-right: 8px;
}

/*Cuando pulsamos en un elemento de la lista, le cambiamos el color*/
.list li:active {
    background-color: #d6d6d6;
}

/*Añadimos para que el header no haga scroll:*/
.scroller {
    overflow: auto;
/*iOS 4 or lower required an esoteric two finger gesture to scroll elements but normality was achieved from iOS 5. Unlike other browsers, while overflow:auto works, momentum scrolling is disabled unless you also add -webkit-overflow-scrolling: touch.*/
    -webkit-overflow-scrolling: touch;
    position: absolute;
    top: 141px;
    bottom: 0px;
    left: 0px;
    right: 0px;
}

.chevron {
    background: transparent url(../img/next_blue.svg);
    background-repeat: no-repeat;
    background-size: contain;
    width: 20px;
    height: 20px;
    position: absolute;
    right: 12px;
    top: 22px;

}
```
