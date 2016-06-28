# PhoneGap



## Introducción
  - Vamos a crear una pequeña práctica con la que aprenderemos las características básicas de Cordova, manejar la API de para usar las características nativas del dispositivo y a crear una aplicación con una arquitectura óptima para móviles.

- Echa un [vistazo primero al diseño y  arquitectura de una aplicación en PhoneGap](http://media.formandome.es/phonegap/presentacion/phonegap_intro.html). Ahí entre otras cosas aclaro las diferencias entre PhoneGap y Cordova.



## Requisitos previos

- En el capítulo de *Entorno de trabajo* vimos como instalar Android Studio junto con el JDK
- Desde el software de Android Studio podemos instalar los SDK de Android que necesitemos.
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
  - El proyecto se ejecuta en el dispositivo físico y si no existe, en el emulador
  
    ```
    cordova run android
    ```

  - El proyecto se ejecuta en el emulador

    ```
    cordova emulate android
    ```
   
  -  Se genera el apk del proyecto, para poderlo instalar "a mano".

    ```
    cordova build android
    ```
 


### Nuestro entorno de desarrollo
- Probaremos todo lo que podamos directamente en el navegador
- Si podemos, utilizamos emulador... aunque **VirtualBox no soporta virtualización anidada**
- Generamos el apk y lo instalamos en el movil
  - Necesitamos **habilitar sideload** (Ajustes->Seguridad->Origenes desconocidos)
  - El apk se puede enviar de forma cómoda mediante **AirDroid** o se puede colgar en una url y acceder vía navegador
  - Para instalarlo basta con hacer doble click
- Utilizaré **Screen Stream Mirroring** para compartir la pantalla


## Práctica de Cordova
- Hacemos un [fork de mi repositorio](https://github.com/juanda99/practica-cordova)
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
xdg-open index.html
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
  
- Al utilizar nuestra aplicación algo nativo, deberemos añadir la librería cordova.js:
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
- Plantilla para la página de inicio (fichero *templates/home.handlebars*):
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
- Plantilla para la lista de futbolistas (fichero *templates/listaJugadores.handlebars*):

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
   $ npm i -g handlebars #en caso de que no tengamos handlebars
   $ handlebars templates/ -f js/templates.js
   ```
   
 - Cambiamos las funciones de app.js para que carguen el template:
 ```
    function renderHomeView() {
      $('body').html(Handlebars.templates.home());
      $('#btnBuscar').on('keyup', encontrarPorNombre);
    }

    function encontrarPorNombre() {
      adapter.encontrarPorNombre($('#btnBuscar').val()).done(function(futbolistas) {
        $("#lstFutbolistas").html(Handlebars.templates.listaJugadores(futbolistas));
      });
    }
  ```
  
- Copiamos el framework de topcoat dentro de nuestro proyecto. Podemos elegir entre un theme claro y otro oscuro.

  ```
  <link href="assets/topcoat/css/topcoat-mobile-light.css" rel="stylesheet">
  ```
- Cargamos también el script de handlebars
   - Al precompilar, cogeremos el runtime, 
   - Utilizo el plugin de Sublime cdnjs 

  ```
  <script src="http://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.0.5/handlebars.runtime.min.js"></script>
  ```
- Cargamos también los templates precompilados:

  ```
  <script src="http://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.0.5/handlebars.runtime.min.js"></script>
  <script src="js/templates.js"></script>
  ```

- Si probamos el resultado, vemos que se le puede dar un toque adicional de diseño. Debemos crear un fichero style.css que añadiremos a nuestro index.html:

  ```
  <link href="assets/css/styles.css" rel="stylesheet">
  ```
- Contenido del fichero *assets/css/styles.css*:

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
  
## Crear una clase vista
- Vamos a dar algo más de estructura a la aplicación, “adelgazando” el fichero app.js. 
- Nos llevaremos toda la lógica de como crear las vistas a otro fichero-clase, HomeView.js, que encapsulará la lógica de creación y renderizado de la vista.
-  Debemos pensar que puede haber muchas vistas, y de este modo, cada una de ellas estará en su propia clase, sin cargar en exceso el núcleo de nuestra aplicación, el fichero app.js.


### Clase HomeView
- Creamos la clase HomeView. El código será el siguiente:

  ```
  var HomeView = function (adapter) {
      this.inicializar = function () {
          // Definimos un div para la vista. Lo usaremos para añadir eventos.
          this.el = $('<div/>');
          this.el.on('keyup', '#btnBuscar', this.encontrarPorNombre);
      };
      this.render = function() {
          this.el.html(Handlebars.templates.home());
          return this.el;
       //esto es lo que hemos movido de app.js aquí:
       //$('body').html(Handlebars.templates.home());
       //La siguiente línea sobra, ya está puesta al inicializar: 
       //$('#btnBuscar').on('keyup', encontrarPorNombre);

      };
      //este método lo movemos tal cual de app.js:
      this.encontrarPorNombre = function() {
          adapter.encontrarPorNombre($('#btnBuscar').val()).done(function (futbolistas) {
             $("#lstFutbolistas").html(Handlebars.templates.listaJugadores(futbolistas)); 
      });
      };
      this.inicializar();
  }
  ```

- Eliminamos las funciones renderHomeView y encontrarPorNombre de app.js
- Cargamos el script de HomeView.js en nuestro index.html antes de cargar app.js:
  ```
  <script src="js/HomeView.js"></script>
  ```
- Modificamos la función de inicialización de app.js para que renderice la vista de inicio mediante la clase HomeView recién creada:

  ```
  adapter.inicializar().done(function () {
    $('body').html(new HomeView(adapter).render());
  });
  ```
  
## Implementar scrolling

- Cuando la lista de futbolistas es mayor que la ventana del navegador, si nos desplazamos, toda la vista hace scrolling (incluido el header).
- Para que el scroll se produzca solo en la lista de futbolistas crearemos una clase adicional en el fichero *assets/css/styles.css* con el siguiente contenido:

  ```
  .scroller {
      overflow: auto;
      -webkit-overflow-scrolling: touch;
      position: absolute;
      top: 141px;
      bottom: 0px;
      left: 0px;
      right: 0px;
  }
  ```
- Añade la clase scroller en el div de la lista de jugadores (plantilla home.handlebars)
  ```
   <div class="topcoat-list scroller">
  ```
  - Por último, ¡no olvides hacer la precompilación del template antes de comprobar el resultado!

## Enrutado de vistas
- Vamos a crear otra vista en la que mostraremos los detalles de cada jugador. 
- Al tener ahora nuestra aplicación más de una vista, habrá que implementar algún mecanismo de enrutado que determine si debemos mostrar la vista de inicio o la de detalle del jugador.


### Implementar vista de jugador
- Creamos nuestra nueva plantilla, mediante el fichero *templates/jugador.handlebars*:

```
   <div class="topcoat-navigation-bar">
        <div class="topcoat-navigation-bar__item left quarter">
            <a class="topcoat-icon-button--quiet back-button" href="#">
                <span class="topcoat-icon topcoat-icon--back"></span>
            </a>
        </div>
        <div class="topcoat-navigation-bar__item center half">
            <h1 class="topcoat-navigation-bar__title">Futbolistas</h1>
        </div>
    </div>
    <div class="detalles scroller">
        <img src="assets/img/{{imagen}}" class="imagen-futbolista">
        <h1>{{nombre}} {{apellido}}</h1>
        <p><strong>Equipo:</strong> {{equipo}} </p>
        <p><strong>Posición: </strong>{{posicion}}</p>
        <p><strong>Dorsal:</strong> {{dorsal}}</p>
        <p><em>{{desc}}</em></p>
        <div class="topcoat-list__container clearfix">
            <ul class="topcoat-list list actions">
                <li class="topcoat-list__item"><a href="tel:+34606606606"><p>Llamar al móvil</p><p>+34606606606</p><div class="action-icon icon-call"/></a></li>
                <li class="topcoat-list__item"><a href="tel:+34606606606"><p>Llamar al fijo</p><p>+34976414141</p><div class="action-icon icon-call"/></a></li>
                <li class="topcoat-list__item"><a href="sms:+34606606606"><p>Enviar SMS</p><p>+34606606606</p><div class="action-icon icon-sms"/></a></li>
                <li class="topcoat-list__item"><a href="mailto:micorreo@gmail.com"><p>Enviar correo electrónico</p><p>micorreo@gmail.com</p><div class="action-icon icon-mail"/></a></li>
                <li class="topcoat-list__item"><a href="#" class="add-location-btn"><p>Añadir posición</p></a></li>
                <li class="topcoat-list__item"><a href="#" class="add-contact-btn"><p>Añadir a contactos</p></a></li>
                <li class="topcoat-list__item"><a href="#" class="change-pic-btn"><p>Hacer una foto nueva</p></a></li>
            </ul>
        </div>
    </div>
 ```
 
- Precompilamos las plantillas al haber creado una nueva:

```
 $ handlebars templates/ -f js/templates.js
```

- Creamos la clase JugadorView con el siguiente contenido (fichero *js/JugadorView.js*):

```
var JugadorView = function(adapter, futbolista) {
    this.inicializar = function() {
        this.el = $('<div/>');
    };
    this.render = function() {
        this.el.html(Handlebars.templates.jugador(futbolista));
        return this.el;
    };
    this.inicializar();
}
```
- Cargamos el script *JugadorView.js* en el fichero *index.html* antes del script *app.js*:

  ```
  <script src="js/JugadorView.js"></script>
  ```

### Enrutado
- La función de enrutado tendrá que ir en el fichero app.js.
- Creamos una variable con la expresión regular que utilizaremos para mostrar o no la vista de un jugador en concreto. La guardaremos en la sección de variables locales del fichero app.js:

  ```
  var futbolistaURL = /^#futbolistas\/(\d{1,})/;
  ```

- Definiremos un nuevo listener para cuando haya cambios en el hash de la url, dentro de la sección registro de eventos del fichero app.js

  ```
  $(window).on('hashchange', route);
  ```

- En la sección de funciones locales, definiremos la función route, que se encargará de enrutar a la vista concreta.

```
  function route() {
    var hash = window.location.hash;
    if (!hash) {
        $('body').html(new HomeView(adapter).render());
        return;
    }
    var match = hash.match(futbolistaURL);
    if (match) {
        adapter.encontrarPorId(Number(match[1])).done(function(futbolista) {
            $('body').html(new JugadorView(adapter, futbolista).render());
        });
    }
 }
 ```
 
- Cambiaremos la lógica de la inicialización del adaptador, para que llame a la función de enrutado (fichero app.js) para que cargue la vista que corresponda en función de la url, en vez de cargar siempre la de HomeView:

```
    adapter.inicializar().done(function () {
        console.log("Inicializado: Adaptador de datos");
        //$('body').html(new HomeView(adapter).render());
        route();
    });
 ```
 
 - He añadido varios varias líneas al fichero *assets/css/style.css* para la nueva vista:
 
  ```
   /*Todo lo siguiente lo añadimos para modificar la presentación de la vista de jugador:*/

  .back-button {
      position: absolute;
      top: 10px;
  }
  .topcoat-icon--back {
      background: url("../img/back_light.svg") no-repeat;
      -webkit-background-size: cover;
      -moz-background-size: cover;
      background-size: cover;
  }
  .detalles {
      margin: auto;
      /*para no utilizar el top que he puesto en scroller:*/
      top: 71px !important;
  }
  .detalles>img {
      float:left;
      margin:10px;
      width: 250px;
      height: 250px;
  }
  .detalles h1 {
      padding: 12px 0px 4px 0px;
      margin: 0px 0px 0px 0px;
      font-size: 1.2rem;
  }
  .detalles p {
      padding: 0px 0px 4px 0px;
      margin: 0px 0px 0px 0px;
  }
  .actions > li > a {
      padding-left: 12px;
  }
  .action-icon {
      position: absolute !important;
      top: 18px;
      right: 20px !important;
      width: 28px !important;
      height: 28px;
  }
  .actions li p:nth-of-type(1) {
      color:  #5DC1FF;
      font-size: 0.9em;
      font-weight: lighter;
  }
  .actions li p:nth-of-type(2) {
      color: inherit;
  }
  .icon-call {
      background: transparent url(../img/call.svg);
      background-repeat: no-repeat;
      -webkit-background-size: cover;
      -moz-background-size: cover;
      background-size: cover;
  }
  .icon-sms {
      background: transparent url(../img/chat.svg);
      background-repeat: no-repeat;
      -webkit-background-size: cover;
      -moz-background-size: cover;
      background-size: cover;
  }
  .icon-mail {
      background: transparent url(../img/email.svg);
      background-repeat: no-repeat;
      -webkit-background-size: cover;
      -moz-background-size: cover;
      background-size: cover;
  }
  .clearfix{
      clear: both;
  }
  ```
  
  - Por último probamos que el enrutamiento funcione y se muestre la nueva vista.
  
## Uso del API de localización
  
- Vamos a mostrar las coordenadas (longitud y latitud) mediante una alerta. 
- En una aplicación real, lo guardaríamos en una base de datos como parte de la información del futbolista y al visualizar la ficha mostraríamos los datos de localización en un mapa.
- Como hacemos llamada a código nativo, no se podrá probar desde un navegador en el PC.


- Lo primero es [mirar la documentación de Cordova](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-geolocation/)
- Añadimos el plugin de geolocalización a nuestro proyecto:

  ```
  cordova plugin add cordova-plugin-geolocation
  ```

- Registramos en la función inicializar() de clase JugadorView un event listener para el evento clic en el elemento de la lista “Añadir Localización” (fichero *js/JugadorView.js*):

  ```
  this.el.on('click', '.add-location-btn', this.addLocation);
  ```


- Registramos también en la clase JugadorView el manejador de evento addLocation:

```
   this.addLocation = function(event) {
    event.preventDefault();
    navigator.geolocation.getCurrentPosition(
        function(position) {
            alert(position.coords.latitude + ',' + position.coords.longitude);
        },
        function() {
            alert('Error obteniendo localización');
        });
    return false;
  };
  ```
  
- Comprobamos su funcionamiento


## Uso del API de contactos
- Vamos a permitir añadir a los futbolistas a nuestra lista de contactos
- Al igual que en el caso anterior, necesitaremos usar un emulador o dispositivo móvil para testear el resultado
- Lo primero es [mirar la documentación de Cordova](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-contacts/index.html)


- Añadimos el plugin:
  ```
  cordova plugin add cordova-plugin-contacts
  ```
- Registramos en la función *inicializar()* de clase JugadorView un event listener para el evento clic en el elemento de la lista “Añadir a Contactos” (fichero *js/JugadorView.js*):

```
   this.el.on('click', '.add-contact-btn', this.addToContacts);
```


- Registramos también en la clase JugadorView el manejador de evento addToContacts:

```
     this.addToContacts = function(event) {
      event.preventDefault();
      console.log('Añadiendo a Contactos');
      if (!navigator.contacts) {
          alert("El API de contactos no está soportada", "Error");
          return;
      }
      /*Según doc de Cordova: https://github.com/apache/cordova-plugin-contacts/blob/master/doc/index.md: */

      // create a new contact object
      var contact = navigator.contacts.create();
      contact.displayName = "Futbolista";
      contact.nickname = "Futbolista";            // specify both to support all devices

      // populate some fields
      var name = new ContactName();
      name.givenName = futbolista.nombre;
      name.familyName = futbolista.apellido;
      contact.name = name;

     // save to device
     contact.save(
        function () {
           alert ("Futbolista guardado en los contactos del teléfono");
        },
        function () {
           alert("uppps, no ha ido bien: " + contactError.code)
        }
     );
   };
 ```
 - Comprobamos su funcionamiento


## Uso del API para la cámara de fotos
- Vamos a limitarnos a capturar una nueva foto, sin guardarla de forma persistente.
- Mira [el funcionamiento de la API en la documentación de Cordova](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-camera/index.html)


- Instalamos el plugin necesario:
  ```
  cordova plugin add cordova-plugin-camera
  ```
- Registramos en la función inicializar() de clase JugadorView un event listener para el evento clic en el elemento de la lista “Hacer una foto nueva” (fichero js/JugadorView.js):
  ```
  this.el.on('click', '.change-pic-btn', this.cambiarFoto);
  ```


- Registramos también en la clase JugadorView el manejador de evento cambiarFoto:

```
    this.cambiarFoto = function(event) {
    event.preventDefault();
    if (!navigator.camera) {
        alert("Camera API no soportada", "Error");
        return;
    }
    var options =   {   quality: 50,
                        destinationType: Camera.DestinationType.DATA_URL,
                        sourceType: 1,      // 0:Photo Library, 1=Camera, 2=Saved Album
                        encodingType: 0     // 0=JPG 1=PNG
                    };
 
    navigator.camera.getPicture(
        function(imageData) {
            $('.imagen-futbolista', this.el).attr('src', "data:image/jpeg;base64," + imageData);
        },
        function() {
            alert('Error al obtener la foto', 'Error');
        },
        options);
 
    return false;
};
```