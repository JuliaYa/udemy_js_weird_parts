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

