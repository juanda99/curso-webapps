# Introducción

## Objetivos del curso

- Configurar entornos reales de trabajo para desarrollo web
    - Editores
    - Control de versiones
    - Automatización de tareas


- Desarrollo Web actual
    - Páginas adaptables
    - Criterio Mobile First
    - Frameworks de CSS: Bootstrap y Material Design
    - Frameworks de JavaScript: React.js


- Conocer arquitecturas de desarrollo de software
    - MEAN stack
    - Real time
    - Aplicaciones embebidas para móviles
    - Web Components
    

- Apreciar la evolución en el desarrollo del software
    - Tests: Mocha, Code coverage, Travis...
    - CSS -> Preprocesado de CSSS -> Frameworks de CSS -> CSS Modules...
    - Uso de transpilers y evolución actual de JavaScript

## Relación con el currículo de DAW

### Sistemas informáticos
- Utilizaremos comandos de consola de Linux
- Ejecución de servicios
- Añadir repositorios e instalar paquetes

### Bases de datos
- Utilizaremos una base documental MongoDB (la opción más extendida)
    - ¡¡¡No aparece en el currículo!!!

### Lenguaje de marcas
- Crear y validar documentos en html

### Programación
- Utilizaremos elementos y estructuras propias de los lenguajes de programación, **mediante JavaScript**

### Entornos de desarrollo
- Arquitectura de aplicaciones Web
    - Api REST
    - Aplicaciones para móviles
- Instalación y uso de entornos de desarrollo
    - Configuración y uso de Sublime Text
    - Otras opciones
    - Entornos de optimización y automatización de tareas mediante con node.js
- Pruebas mediante Mocha
- Control de versiones

### Despliegue y aplicaciones Web
- Instalación de un servidor Web 
    - Express y node.js
- Control de versiones

### Desarrollo Web en entorno Servidor
- Arquitectura de aplicaciones Web
- Api REST
    - Soluciones híbridas
    - Soluciones en tiempo real
    - ¡Nada de etiquetas embebidas: asp, php...

### Desarrollo Web en entorno Cliente
- Repaso general de todo el temario

### Diseño de interfaces Web
- Repaso general de todo el temario




- [Instalación y configuración de Sublime Text 3 en Ubuntu 14.04 para desarrollo Web](http://www.formandome.es/linux/instalacion-y-configuracion-de-sublime-text-3-en-ubuntu-14-04-para-desarrollo-web/)

```
sudo add-apt-repository ppa:webupd8team/sublime-text-3 
sudo apt-get update
sudo apt-get install sublime-text-installer
```

### Instalación de Google Chrome
- [Desde la web](https://www.google.com/chrome/browser/desktop/index.html)

### Instalación de Adobe Brackets
- [Web de referencia](http://brackets.io/)
- Es un editor exclusivamente para web (js, html, css)
- [Más información](http://www.formandome.es/linux/instalacion-y-configuracion-de-brackets-en-ubuntu-14-04/)
- 
### Instalación de Gnome Shell
- [Como instalarlo y configurarlo](http://www.formandome.es/linux/configuracion-inicial-de-ubuntu-14-04/)
- Instalaremos también un terminal: Guake

### Instalación de MongoDB
- [Instalaremos primero mongodb](https://docs.mongodb.com/master/tutorial/install-mongodb-on-ubuntu/):
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

- El servicio se levanta como otros servicios de Linux: 
```
sudo service mongod start
```

- Y para entrar a su consola, mediante **mongo**, o mediante algún gui como por ejemplo [Robomongo](https://robomongo.org/)

