# Creación de una API con node.js



## Primeros pasos
- npm configurado y git configurado
- Crear repositorio en GitHub
- Clonar repositorio
- Ejecutar npm init
- Crear la estructura de la aplicación, por el momento una carpeta app donde iremos guardando el código propio de la aplicación


## Configuración de eslint
- Si tienes los linters para Sublime y js configurados, comprueba que la consola arroja un error.
- 
- Hay que configurar eslint para formatear nuestro código.

  ```
  npm i -D eslint
  ```

- Como lo instalo en local, para ejecutarlo, necesito darle el path:
```
./node_modules/.bin/eslint --init
? How would you like to configure ESLint? Answer questions about your style
? Are you using ECMAScript 6 features? No
? Where will your code run? Node
? Do you use JSX? No
? What style of indentation do you use? Spaces
? What quotes do you use for strings? Single
? What line endings do you use? Unix
? Do you require semicolons? No
? What format do you want your config file to be in? JSON
Successfully created .eslintrc.json file in /home/juanda/api_node_express/ejercicio3-nodemon-eslint
```

## express
- Utilizaremos [express](http://expressjs.com/es/) para realizar la API
- Instalar express mediante uno de los comandos siguientes:
  ```
npm install --save express
npm i -S express
```
- Creamos el fichero app/server.js donde pondremos el código necesario para testear una API muy básica para probar Express.

- Utiliza el plugin ExpressComplete (aget, aput...) de Sublime para autocompletado

  ```
  var express = require('express'); //llamamos a Express
  var app = express();                

  var port = process.env.PORT || 8080;  // establecemos nuestro puerto

  app.get('/', function(req, res) {
      res.json({ mensaje: '¡Hola Mundo!' });   
  });
  
  app.get('/cervezas', function(req, res) {
      res.json({ mensaje: '¡A beber cerveza!' });   
  });
  
  app.post('/', function(req, res) {
      res.json({ mensaje: 'Método post' });   
  });
  
  app.del('/', function(req, res) {
      res.json({ mensaje: 'Método delete' });   
  });

  // iniciamos nuestro servidor
  app.listen(port);
  console.log('API escuchando en el puerto ' + port);
  ```

- Comprueba que el linter de JavaScript te funcione bien, si da un error en console.log, puedes deshabilitar esa regla en el fichero de configuración de eslint (*no-console: 0*)

- Iniciamos nuestro API Server mediante el comando 
```
node app/server.js
```

Probamos que la API funcione mediante http://localhost:8080 o utilizando la extensión de Google Chrome **Postman**

- Para homogeneizar, vamos a crear un script en nuestro fichero package.json, de modo que podamos arrancar nuestra API mediante ```npm start```

```
"start": "node app/server.js"
```

- Vamos a tener todas nuestras rutas separadas, mediante el uso de enrutadores.
  - Esto nos permite una configuración más sencilla por cada ruta
  - Podremos hacer de forma sencilla un versionado de API
  - 

  // para establecer las distintas rutas, necesitamos instanciar el express router
  var router = express.Router();              

  //establecemos nuestra primera ruta, mediante get.
  router.get('/', function(req, res) {
      res.json({ mensaje: '¡Hola Mundo!' });   
  });

  // nuestra ruta irá en http://localhost:8080/api
  // es bueno que haya un prefijo, sobre todo por el tema de versiones de la API
  app.use('/api', router);

## Recibir parámetros
- Cuando el router recibe una petición, podemos observar que ejecuta una función de callback *function (req, res)*:
    -  El parámetro **req** representa la petición (request) 
    -  El parámetro **res** representa la respuesta (response), que en el caso anterior hemos codificado en json.


- A menudo la petición se hará enviando algún parámetro adicional. Hay varias posibilidades:
    - Mediante la url: se recogerán mediante req.param.nombreVariable
    - Mediante post en http hay dos posiblidades:
        - application/x-www-form-urlencoded
        - multipart/form-data
- En peticiones post, [escogeremos x-www-form-urlencoded si no se envía una gran cantidad de datos (normalmente ficheros)](http://stackoverflow.com/questions/4007969/application-x-www-form-urlencoded-or-multipart-form-data) 


## Parámetros por url
- Vamos a mandar un parámetro *nombre* a nuestra api, de modo que nos de un saludo personalizado.

```
router.get('/:nombre', function(req, res) {
    res.json({ mensaje: '¡Hola' + req.params.nombre });   
});
```


## nodemon
- Es un wrapper de node, para reiniciar el servidor de apis cada vez que detecte modificaciones.

```
npm i -D nodemon
```

- Cada vez que ejecutemos **npm start** ejecutaremos nodemon en vez de node. Habrá que cambiar el script en el fichero *package.json*:

```
"start": "nodemon app/server.js"
```


## Parámetros por post
- Parámetros mediante **POST y application/x-www-form-urlencoded**:
    - Necesitaremos [body-parser](https://www.npmjs.com/package/body-parser): extrae los datos del body y los convierte en json
- Parámetros mediante **POST y multipart/form-data**
    - Usaremos [https://www.npmjs.com/package/busboy](https://www.npmjs.com/package/busboy) o [Multer](https://github.com/expressjs/multer) 


## Ejemplo con body-parser
- Hay que instalar body-parser
```
npm i -S body-parser
```

- body-parser actúa como middleware. 
- El código adicional será similar al siguiente:

```
var bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: true }))
app.use(bodyParser.json())
```

- Una forma buena para testear el funcionamiento es instalar una extensión de Chrome: [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)


## Rutas de nuestra API REST

- Las rutas que utilizaremos son las siguientes:

| Ruta     | Verbo http    |  Cool |
|----------|:-------------:|------|
| /api/cervezas |  GET | Obtenemos todas las cervezas |
| /api/cervezas/q=keyword |  GET | Obtenemos cervezas por keyword |
| /api/cervezas/:id |  GET | Obtenemos los datos de una cerveza |
| /api/cervezas | POST | Damos de alta una cerveza |
| /api/cervezas/:id | PUT | Actualizamos los datos de una cerveza |
| /api/cervezas/:id | DELETE | Borramos los datos de una cerveza |


## Acceso a base de datos
- Para la persistencia de nuestros datos utilizaremos una base de datos
- Optamos por una base de datos MongoDB:
    - Es lo más habitual en arquitecturas MEAN
    - Así operamos con objetos json tanto en node como en bbdd (bson)
    - Nos permite más libertad, al utilizar colecciones en vez de tablas


## Instalación de MongoDB
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

- La consola de Mongo también es un intérprete de JavaScript :-)


## Inserción de datos

- Utilizaremos el fichero *cervezas.json*
- Importar nuestro cervezas.json a una base de datos
```
mongoimport --db test --collection cervezas --drop --file cervezas.json --jsonArray
```


- Para poder hacer una búsqueda por varios campos de texto, tendremos que hacer un índice:
```
db.cervezas.createIndex(
   {
     "Nombre": "text",
     "Descripción": "text"
   },
   {
     name: "CervezasIndex", 
     default_language: "spanish" 
   }
)
```
- Comprobamos que el índice esté bien creado
```
db.cervezas.getIndexes()
```
- Si hiciera falta, lo podemos recrear:
```
db.cervezas.dropIndex("CervezasIndex")
```


## Instalación de Mongoose

- Instalaremos [mongoose] como ODM (Object Document Mapper) en vez de trabajar con el driver nativo de MongoDB (se utiliza por debajo).
```
npm i -S mongoose
```


## Uso de Mongoose
- Incluir Mongoose y abrir una conexión:
```
var mongoose = require('mongoose')
mongoose.connect('mongodb://localhost/test')
```

- Usar la conexión:

  ```
  var mongoose = require('mongoose')

  var MONGO_URL = process.env.MONGO_URL || 'mongodb://localhost/cervezas'
  mongoose.connect(MONGO_URL)

  mongoose.connection.on('connected', function () {
    console.log('Conectado a la base de datos: ' + MONGO_URL)
  })

  mongoose.connection.on('error',function (err) {
    console.log('Error al conextar a la base de datos: ' + err)
  })

  mongoose.connection.on('disconnected', function () {
    console.log('Desconectado de la base de datos')
  })

  process.on('SIGINT', function() {
    mongoose.connection.close(function () {
      console.log('Desconectado de la base de datos al terminar la app')
      process.exit(0)
    })
  })
  ```

- Definir un esquema para nuestros objetos (cervezas) y crear nuestro modelo a partir del esquema:

  ```
  var mongoose = require('mongoose')
  var Schema = mongoose.Schema

  var cervezaSchema = new Schema({
    Nombre: String, 
    Descripción: String, 
    Graduacion: String,
    Envase: String,
    Precio: String 
  })

  var Cerveza = mongoose.model('Cerveza', cervezaSchema)

  module.exports = Cerveza
  ```
 

- Ahora podríamos crear documentos y guardarlos en la base de datos:

  ```
  var miCerveza = new Cerveza({ name: 'Ambar' });
  miCerveza.save(function (err, miCerveza) {
    if (err) return console.error(err);
    console.log('Guardada en bbdd' + miCerveza.name);
  })
```

- Vamos a guardar las cervezas en la bbdd


¿Me falta aquí algo de documentación?


## Test de la API
- Utilizaremos [Mocha](https://mochajs.org/) como test framework y [supertest](https://github.com/visionmedia/supertest) para hacer las peticiones http.

```
npm i -D mocha supertest
```
- Creamos nuestro fichero *tests/api.test.js* con la prueba para crear una cerveza:

```
'use strict'
/* global describe it */
var request = require('supertest')

/*obtenemos nuestra api rest que vamos a testear*/
var app = require('../app/server')

describe('Crear una nueva cerveza', function() {
  it('Crea la cerveza retornando 201', function(done) {
    request(app)
      .post('/api/cervezas/')
      .set('Accept', 'application/json')
      .expect('Content-Type', /json/)
      .send({
        'Nombre': 'DAMN',
        'Descripción': 'Mi cerveza preferida',
        'Graduación': '10º',
        'Envase': 'Bidón',
        'Precio': '1 eurito'
      })
      .expect(201, done)
  })
})
```

- Utiliza los paquetes **Mocha Snippets** y **Chai Completions** de Sublime Text para completar el código

- Si echamos un vistazo al código anterior:
-  **describe** nos sirve para describir los test suites (se pueden anidar varios)
  - **it** nos sirve para describir cada caso de test. 
  - **requests(app).post** realizará una petición post a nuestra api

- ¿Cómo ejecutamos el test?
  - Mediante línea de comandos (hace falta la ruta completa ya que no hemos instalado el paquete de forma global):
  
  ```
  node_modules/.bin/mocha tests
  ```
  - Introduciendolo en el fichero package.json (no hace falta la ruta al estar dentro del package.json):
  ```
   "test": "mocha tests"
  ```
- Para que el caso anterior funcione, tenemos que modificar nuestro fichero *app/server* de modo que se pueda utilizar *app* desde otro fichero js:
```
/*lo añado al final de app/server.js:*/
module.exports = app
```

- Por último podríamos utilizar un paquete como **istanbul** que nos analice el código y ver si nuestras pruebas recorren todas las instrucciones, funciones o ramas del código:
``` 
./node_modules/.bin/istanbul cover -x "**/tests/**"  ./node_modules/.bin/_mocha  tests/api.test.js
```

- Estos datos son facilmente exportables a algún servicio que nos de una estadística de la cobertura de nuestros tests o que haga un seguimiento de los mismos entre las distintas versiones de nuestro código.
- 
- Por último también se podría integrar con un sistema de integración continua tipo Travis.

