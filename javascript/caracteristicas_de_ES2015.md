# Características de ES2015


## Arrow functions
- Para escribir funciones de forma rápida. Esta característica está presente en otros lenguajes. También se conoce como lambdas.

```
var salary = [10000, 20000, 30000];
var with1000Increment = salary.map(x => x + 1000);
console.log(with1000Increment);
// > [11000, 21000, 31000];
```
[Ver código](https://goo.gl/Tc0BV4)

Si hubiera más de un argumento, son necesarios paréntesis:
```
var marks = [89, 10, 70];
marks = marks.sort((a, b) =>  b - a);
console.log(marks);
// > [89,70,10]
```
[Ver código](https://goo.gl/08Ilik)

Arrow Functions to Avoid the "self" Madness

If you are writing JavaScript, I hope you know what "self" is and how ugly it is. We can easily avoid it with arrow functions.

Here's a stupid example trying to console.log all the meta tags after 100 milliseconds:

$('meta').each(function() {
    setTimeout(() => {
        console.log(this.name);
    }, 100);
});
Live Code: https://goo.gl/xUrZSG
If there were no arrow functions, we would need to write it like this:

$('meta').each(function () {
    var self = this;
    setTimeout(function () {
        console.log(self.name);
    }, 100);
});

## Creación de objetos
- Se reduce la sintáxis para la creación de objetos:

```
var name = "Arunoda";
var user = {
    name,
    getAddress() {
        return "Colombo. Sri Lanka";
    }
};
```
[Ver código](https://goo.gl/9VMfoS)

Antes de ES2015 se hubiera escrito así:
```
var name = "Arunoda";
var user = {
    name: name, 
    getAddress: function() {
        return "Colombo. Sri Lanka";
    }
};
```
## Variables en cadenas
Desde ES2015 se evita la necesidad de utilizar el operador de concatenación (+):

```
var name = "Arunoda";
var address = "Colombo, Sri Lanka";

var greeting = `My Name is ${name} and I live in ${address}`;
alert(greeting);
// Note the use of "`" character
```
[Ver código](https://goo.gl/zfUzWq)

También en multilínea:

```
var blogPost = `
    ## My First Blog Post 

    I like to write in Markdown!   
`
```
[Ver código](https://goo.gl/GbbmHD)

Destructuring and Matching

With this feature, you can reduce the amount of code and self-document it.

Let's say we have a user object and we are only interested in the name field. This is how we can do it with ES2015:

var user = {name: "arunoda", address: "Colombo. Sri Lanka"};
var {name} = user;
console.log(name);
This seems kind of weird at first. But it’s very useful when you are working on a real app. Let's say I want to get the target of a click event. Here's how:

$("body").click(function({target}) {
    console.log(`You clicked on ${target}`);
});
Live Code: https://goo.gl/uFwzx8
You can also use this to self-document code when accepting an object into an API. For example, let’s say I have a function that accepts an object that has name and address. Then it prints a greeting. This is how we can do it with destructors:

function GreetUser({name, address="N/A"}) {
  console.log(`${name}'s address is: ${address}`);
}

GreetUser({name: "Arunoda"});
Live Code: https://goo.gl/OgWhrD
Argument Spreading and the Rest Operator

In JavaScript, we can accept any number or arguments. But this feature is kind of difficult to handle. ES2015 makes it pretty simple.

Let's implement a function like Meteor.subscribe:

function MySubscribe(name, ...params) {
    var paramsString = params.join(", ");
    console.log(`Subscribing to ${name} with "${paramsString}"`);
}


MySubscribe("getPost", "meteor-category", "postId");
Live Code: https://goo.gl/zLDEKi
You can also use the spread operator to pass an array of arguments to a function. See:

function MySubscribe(name, ...params) {
    var paramsString = params.join(", ");
    console.log(`Subscribing to ${name} with "${paramsString}"`);
}

var params = ["meteor-category", "postId"];
MySubscribe("getPost", ...params);
Live Code: https://goo.gl/zAx2uf

