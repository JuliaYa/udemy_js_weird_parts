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
