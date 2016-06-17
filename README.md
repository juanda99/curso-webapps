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



## Conocimientos previos


- html, css y js básico
- Puedes seguir este [tutorial para html y css básico](http://www.media.formandome.es/inaem/html/export/html-reveal-slides.html)
- Empezaremos con un ejercicio práctico:
  - Nos familiarizamos con Sublime Text
  - Practicamos con Emmet
  - Repasamos Chrome Developer Tools
  - Repasamos etiquetas html5 y css



## Relación con el currículo de DAW


### Sistemas informáticos
- Utilizaremos comandos de consola de Linux
- Ejecución de servicios
- Añadir repositorios e instalar paquetes


### Bases de datos
- Utilizaremos una base documental MongoDB (la opción más extendida)
    - ¡¡¡No aparece en el currículo!!!
- Quizá algún ejercicio con MySql y phpMyAmin


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
- Pruebas mediante [Mocha](https://mochajs.org/)
- Integración continua mediante [Travis CI](https://travis-ci.org/)
- Code Coverage con [istanbul](https://github.com/gotwarlost/istanbul)
- Control de versiones con [Git](https://git-scm.com/) y [GitHub](https://github.com/)


### Despliegue y aplicaciones Web
- Instalación de un servidor Web 
    - Express y node.js
- Control de versiones con [Git](https://git-scm.com/) y [GitHub](https://github.com/)


### Desarrollo Web en entorno Servidor
- Arquitectura de aplicaciones Web
- Api REST
    - Soluciones híbridas
    - Soluciones en tiempo real
    - ¡Nada de etiquetas embebidas: asp, php...!


### Desarrollo Web en entorno Cliente
- Repaso general de todo el temario


### Diseño de interfaces Web
- Repaso general de todo el temario



## Cómo trabajar


### Roles
![](chiste.gif)


- ¿Quién es el profesor?
  - Persona con conocimientos límitados 
  - Tiempo de respuesta: ¿horas? ¿días?
  - Buen orientador


- ¿Quién es [stackoverflow](http://stackoverflow.com/)?
  - Multitud de personas con múltiples conocimientos (ver tags)
  - Tiempo de respuesta: ¿minutos?
  - La mejor herramienta junto con GitHub para ir haciendo curriculum


### Trabajo por proyectos
- Complicado con los módulos si los hacemos "estancos"
- Fomenta la creatividad y el trabajo en equipo
- Que trabajen los alumnos. Es más interactivo y menos cansado :-)
- Los controlamos mediante GitHub o Bitbucket
  - Repositorios privados o públicos
  - PR en vez de copiarse del compañero
  - Tiene que estar claro como funciona desde 1º y no hay otra forma que haciendo código


### Otras ideas
- Servidor en la nube
  - [So You Start](http://www.soyoustart.com/es/) con [Vesta](https://vestacp.com/)
  - Primer portfolio del alumno
  - Entorno real
- [Virtualiza con Docker](https://www.docker.com/)
  - Más rápido
  - Se puede montar un [servidor de imágenes Docker en el propio centro](http://www.media.formandome.es/markdownslides/docker/export/docker-reveal-slides.html) 
- Uso de gestores de contenidos ([Wordpress](https://wordpress.com/), [Joomla](https://www.joomla.org/), [Magento](https://magento.com/), [Prestashop](https://www.prestashop.com/es/))...



## Documentación
- **[Generada con Gitbook](https://www.gitbook.com)**
- Para generar las slides, pdf, epub o mobi
  - Es necesario tener instalado calibre

  ```
  git clone git@github.com:juanda99/curso-webapps.git
  cd curso-webapps
  gitbook install
  npm install
  npm run slides
  npm run pdf
  npm run epub
  npm run mobi
  ```

- [Libro online](https://www.gitbook.com/book/juanda/webapps/details) con generación de pdf, epub y mobi