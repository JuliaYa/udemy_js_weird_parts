## Objects and the Dot

### Object

- Primitive "property"
- Object "property
- Function "method"

Object (core object) will have some sort of address in computer's memory. And it will have references to these different properties and methods (they addresses in memory. Now they may be related to the address of that base object concept, or they may not.

```javascript
var person = new Object();    // not the best way to create object

// '[]' operator that find or create property
person["firstname"] = "Tony";   
person["lastname"] = "Alicea";

var firstNameProperty = "firstname";

console.log(person);
console.log(person[firstNameProperty]);

console.log(person.firstname);
console.log(person.lastname);

// '.' operator that find or create property
person.address = new Object();
person.address.street = "111 Main St."; 
person.address.city = "New York";
person.address.state = "NY";

console.log(person.address.street);
console.log(person.address.city);
console.log(person["address"]["state"]);
```
'.' operator preferable to use, because it's very clean and it's also easier to debug and find problems.


## Objects and Object literals

```javascript
// object literal, not operator
let Tony = { 
  firstname: 'Tony',
  lastname: 'Alicea',
  address: {
    street: '111 Main St.',
    city: 'New York'
    state: 'NY'
  }
};
```
We can set up properties and methods, all within curly braces on what is essentially treated as one line of code.

JS is very liberal about letting you use white space that is spaces and tabs and carriage returns, and this still treated as one line of code. Syntax parser and JS engine when it hits this line of code understand it as object creation.

We can create an object anywhere that We can create any other variable on the fly.

```javascript
function greet(person){
  console.log('Hi' + person.firstname);
}
greet(Tony);  // => Tony
greet({
  firstname: 'Mary',
  lastname: 'Doe'
});   //    => Mary
```
We can add properties after creating with object literal.

```javascript
Tony.address2 = {
  street: '333 Second St.'
};
```
**Object literals syntax turns out to be really powerful. It can make some very clean looking, readable and easy to write code.**

## Faking namespaces

**Namespace** - container for variables and functions. Typically to keep variables and functions with the same name separate

JS doesn't have namespaces. But we don't need it, we can fake it.

```javascript
var greet = 'Hello!';
var greet = 'Hola!';

console.log(greet); // => Hola!
```

To avoid this behavior we can use objects as containers.

```javascript
  var english = {};
  var spanish = {};

  english.greet = 'Hello!';
  spanish.greet = 'Hola!';

  console.log(english); // => Object {greet: 'Hello!'}
```

And we can keep having levels of different containing objects.

## JSON and Object Literals

**JSON** - JavaScript Object Notation
It's inspired by object literal syntax in JS.

Common mistake is to think that they're the exact same thing and run across some errors.

```javascript
var objectLiteral = {
  firstname: 'Julia',
  isAProgrammer: true
}
```

Before JSON data was sent like this (xml format):

```xml
<object>
  <firstname>Julia</firstname>
  <isAProgrammer>true</isAProgrammer>
</object>
```
But for big arrays of data it was too much unnecessary characters that make the amount of data larger. Download time matters.

String like this much faster, only difference is quoted property names:

```json
{
  "firstname": "Julia",
  "isAProgrammer": true
}
```

So JSON is technically a subset of the object literal syntax. Valid JSON is valid JS object literal syntax.

For all objects we can do: 
```javascript
JSON.stringify(objectLiteral); // convert object to JSON
JSON.parse(JSONString); // convert JSON string to object
```

## Function are Objects

**First class functions** - everything you can do with other types, you can do with functions. Assign them to variables, pass them around, create them on the fly.

Function a special type of object and we can attach properties and methods to it.

In JS the function object has some hidden special properties:

* **NAME** optional (can be anonymous)
* **CODE** (code what you write inside) - invocable ()

```javascript
function greet(){
  console.log('hi');  // placed to CODE property
}
greet.language = 'english'; // just custom property
```

## Function statements and function expressions

**Expression**: a unit of code that results in a value. It doesn't have to save to a variable (`2 + 3`).

**Statement** doesn't return value:

```javascript
if (a === 3) {
  ...
}
function greet() {
  console.log('hi);
}
```

***Function expression:***
```javascript
var anonymousGreet = function() {
  console.log('hi);
}
anonymousGreet();
```

But in this case we can't invoke function before initialisation.


## By Value vs By Reference

**by value**

```javascript
var a = 5; // primitive value (one spot in memory)

var b = a; // copy of primitive value (another spot in memory)

a = 2;
console.log(a);   // 2
console.log(b);   // 5 
```

**by reference** for objects (including functions)

```javascript
var myObject = {name: 'Julia', book: 'Harry Potter'};
var copyOfMyObject = myObject;
var otherCopy = myObject;

copyOfMyObject.name = 'Judy';     // mutate
console.log(myObject.name);  // => Judy
console.log(copyOfMyObject.name); // => Judy
console.log(otherCopy.name); // => Judy

function changeObjName(obj) {
  obj.name = 'Hanna';
}

otherCopy = { name: 'Kate' };   // creating other object
changeObjName(myObject);
console.log(myObject.name);  // => Hanna
console.log(copyOfMyObject.name); // => Hanna
console.log(otherCopy.name); // =>  Kate
```
Variables `myObject` and `copyOfMyObject` points to the same place in memory.

**Mutate**: to change something.
**Immutable** means it can't be changed.

The same thing happens for functions.

 ### All objects interact **by reference**.

## Objects, functions and 'this'

`this` can be pointing at a different thing depending on how the function invoked. There are few scenarios where `this` will be changed depending on how the function called.

```javascript
function a() {
  console.log(this);
}

var b = function () {
  console.log(this);
  this.newVariable = 'Hello';
}

var c = {
  name: 'The c object',
  log: function() {
    var self = this;  //  common practice to save this inside object method
    self.name = 'Updated name';
    //this.name = 'Updated name';
    console.log(this);

    var setName = function(newName) {
     // this.name = newName;    // point to Global object Window
      self.name = newName;
    };
    setName('Updated again!');
    console.log(self);    // object c without changes
  }
}

a();  // => Window
b();  // => Window
console.log(newVariable)  // Hello
c.log();    // => Object c
```
we can change object properties from methods inside the object.

## `arguments` and spread

**Arguments**: the parameters you pass to a function.
JS gives you a keyword of the same name which contains them all.

```javascript
function greet(firstname, lastname, language) {
  console.log(firstname);
  console.log(lastname);
  console.log(language);
};
greet();  // undefined undefined undefined
greet('John', 'Doe') // John Doe undefined
```

In JS we can call function with any number of parameters.

To check it inside the function we can do:
```javascript
function greet(firstname, lastname, language) {
 
  language = language || 'en';
  
  if (arguments.length === 0) {
      console.log('Missing parameters!');
      console.log('-------------');
      return;
  }
  
  console.log(firstname);
  console.log(lastname);
  console.log(language);
  console.log(arguments);
  console.log('arg 0: ' + arguments[0]);
  console.log('-------------'); 
}
```
### Spread operator

```javascript
function greet(firstname, lastname, language, ...other) {
  console.log(other);
};
greet('John', 'Doe', 'es', 'Marta', 'en') // => ['Marta', 'en']
```
`other` - extra parameters that aren't defined explicitly wrapped into array.
This approach doesn't available in all browsers yet.

## Function overloading

In JS we doesn't have possibility to overload functions, but we can do it in a few other ways:

The simple one:
```javascript
function greet(firstname, lastname, language) {    
  language = language || 'en';
  
  if (language === 'en') {
      console.log('Hello ' + firstname + ' ' + lastname);   
  }
  
  if (language === 'es') {
      console.log('Hola ' + firstname + ' ' + lastname);   
  }
}

function greetEnglish(firstname, lastname) {
    greet(firstname, lastname, 'en');   
}

function greetSpanish(firstname, lastname) {
    greet(firstname, lastname, 'es');   
}

greetEnglish('John', 'Doe');
greetSpanish('John', 'Doe');
```

## Syntax Parsers

Reads your code and determines if it's valid and what it is trying to do. It's going through your code character by character, making assumptions, stating certain rules, and can even make changes to your code before it's executed. And it's really important to remember it.


## Automatic Semicolon Insertion
Semicolon is optional because JS Engine putting them where it thinks they should be, if they're missing. This can cause a big problem in your code.

Rules:
1. Always put your own semicolons.

```javascript
function getPerson() {
  return        // parser put semicolon after return
  {
    firstname: 'Tony'
  }
}
console.log(getPerson());   // => undefined
```

## Whitespace
Invisible characters that create literal 'space' in your written code. Carriage returns, tabs, spaces.

```javascript
var 
  // first name of the person
  firstname,

  // last name of the person
  lastname,

  // the language
  // can be 'en' or 'es'
  language;

var person = {
  // some note
  firstname: 'Julia',
  // another note
  lastname: 'Ya'
};

console.log(person);    // => { Object }
```
We can put whitespace, returns and tabs almost everywhere.
***You should do this to make your code more readable for yourself and other developers.***

## Immediately Invoked Functions Expressions (IIFEs)

```javascript
// function statement
function greet(name) {
    console.log('Hello ' + name);   
}
greet('John');

// using a function expression
var greetFunc = function(name) {
    console.log('Hello ' + name);
};
greetFunc('John');

// using an Immediately Invoked Function Expression (IIFE)
var greeting = function(name) {
    
    return 'Hello ' + name;
    
}('John');

console.log(greeting);

// IIFE
var firstname = 'John';

(function(name) {
    
    var greeting = 'Inside IIFE: Hello';
    console.log(greeting + ' ' + name);
    
}(firstname)); // IIFE

```
We only use `()` as a grouping operator and when we use it to wrap anonymous function. In that case engine will think we just creating function object on the fly. Without it we'll get an error.

```javascript
// it's all valid and placed to a memory but kinda lost
3;
"I'm a string";

// we can use this trick
(function(name) {
  console.log('Hello ' + name);  
}(name);)
```

## IIFEs and Safe code

```javascript
(function(name) {
    
    var greeting = 'Hello';    // not in global object
    console.log(greeting + ' ' + name);
    
}(firstname));
```
For this function engine creating new Execution Context, this code will be separate from other code


## Understanding closures

```javascript
function greet(whattosay) {

   return function(name) {
       console.log(whattosay + ' ' + name);
   }

}

var sayHi = greet('Hi'); 
sayHi('Tony');
```

JS engine creates EC for `greet` function and return other function, than remove EC but saves variables in memory for a while. Than engine creates EC for `sayHi` function and run it. Variable `whattosay` still have link to memory with saved value. And all run good.

But here is an example that shows how easily your can make mistakes without understanding closures.

```javascript
function buildFunctions() {
 
    var arr = [];
    
    for (var i = 0; i < 3; i++) {
        
        arr.push(
            function() {
                console.log(i);   
            }
        )
        
    }
    
    return arr;
}

var fs = buildFunctions();

fs[0]();  // => 3
fs[1]();  // => 3
fs[2]();  // => 3

// this is because memory keeps value i = 3 (last cycle run)

// we can avoid it like this
function buildFunctions2() {
 
    var arr = [];
    // es5 approach
    for (var i = 0; i < 3; i++) {
        arr.push(
            (function(j) {
                return function() {
                    console.log(j);   
                }
            }(i))
        )
    }

    // es6 approach
    for (var i = 0; i < 3; i++) {
        let j = i;
        arr.push(
          function() {
              console.log(j);   
          }
        )
    }
    
    return arr;
}

var fs2 = buildFunctions2();

fs2[0]();   // => 0
fs2[1]();   // => 1
fs2[2]();   // => 2
```

## Function Factories

```javascript
function makeGreeting(language) { // function factory
 
  return function(firstname, lastname) {    
    if (language === 'en') {
        console.log('Hello ' + firstname + ' ' + lastname);   
    }
    if (language === 'es') {
        console.log('Hola ' + firstname + ' ' + lastname);   
    }   
  }
}

// makeGreetings calls two times with different EC

var greetEnglish = makeGreeting('en');  // closure with language = 'en'
var greetSpanish = makeGreeting('es');  // closure with language = 'es'

greetEnglish('John', 'Doe');  // => Hello John Doe
greetEnglish('Jane', 'Doe'); // => Hello Jane Doe
greetSpanish('John', 'Doe');  // => Hola John Doe
```
**Every time when call a function we get new EC with own variable environment**

## Closures and Callbacks

**Callback function**: a function you give to another function, to be run when the other function is finished. So the function you call (invoke), 'calls back' by calling the function you gave it when it finished.

```javascript
function sayHiLater() {
 
    var greeting = 'Hi!';
    
    setTimeout(function() {
        
        console.log(greeting);
        
    }, 3000);
    
}

sayHiLater();

// jQuery uses function expressions and first-class functions!
//$("button").click(function() {
//    
//});

function tellMeWhenDone(callback) {
 
    var a = 1000; // some work
    var b = 2000; // some work
    
    callback(); // the 'callback', it runs the function I give it!
    
}

tellMeWhenDone(function() {
   
    console.log('I am done!');
    
});

tellMeWhenDone(function() {
   
    console.log('All done...');
    
});

```

## call(), apply() and bind()

```javascript
var person = {
    firstname: 'John',
    lastname: 'Doe',
    getFullName: function() {
        
        var fullname = this.firstname + ' ' + this.lastname;
        return fullname;
        
    }
}

var logName = function() {
  console.log('Logged: ' + this.getFullName())  
}

var logPersonName = logName.bind(person);
logPersonName();  // => Logged: John Doe
```
`bind()` creates copy of function and give it an object that function can treat like `this`.


```javascript
var logName = function(lang1, lang2) {

    console.log('Logged: ' + this.getFullName());
    console.log('Arguments: ' + lang1 + ' ' + lang2);
    console.log('-----------');
    
}

var logPersonName = logName.bind(person);
logPersonName('en');  // => Logged: John Doe / Arguments: en undefined
```
`call()` point to `this` and execute function, not creating a copy

```javascript
logName.call(person, 'en', 'es'); // => Logged: John Doe / Arguments: en es 
```

```javascript
// apply() takes an array of parameters and it's ony difference from call()
logName.apply(person, ['en', 'es']); // => Logged: John Doe / Arguments: en es

(function(lang1, lang2) {

    console.log('Logged: ' + this.getFullName());
    console.log('Arguments: ' + lang1 + ' ' + lang2);
    console.log('-----------');
    
}).apply(person, ['es', 'en']); // => .../ Arguments: es en

// function borrowing
var person2 = {
    firstname: 'Jane',
    lastname: 'Doe'
}

console.log(person.getFullName.apply(person2)); // => Logged: John Doe 

// function currying
function multiply(a, b) {
    return a*b;   
}

var multipleByTwo = multiply.bind(this, 2); // a will be permanently set to 2
console.log(multipleByTwo(4));  // => 8

var multipleByThree = multiply.bind(this, 3); // a will be permanently 3
console.log(multipleByThree(4));  // => 12
```

**Function currying**: creating a copy of a function but with some preset parameters. This is very useful in mathematical problems.