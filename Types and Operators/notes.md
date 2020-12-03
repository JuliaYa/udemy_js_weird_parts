## Types and JavaScript

**Dynamic typing**: you don't tell the engine what type of data a variable holds, it figures it out while your code is running. Single variable can hold different types of values because it's all figured out during execution.

```java
bool myVar = 'hello' // an error
```

```javascript
  let myVar = true; // no errors
  myVar = 'Hey!';
  myVar = 5;
```

This turns out to be quite powerful, and can also cause you some problems if you don't understand how JS is going to make decisions as a result of dynamic typing.


## Primitive types

Primitive type: a type of data that represents a single value. That is not an object.

There are six types in JavaScript.

***Undefined*** - represents lack of existence. JS engine sets variables to initially and it will stay undefined unless you set the variable to have a value.

**(DON'T SET A VARIABLE TO THIS!)**

***NULL*** represents lack of existence

**You CAN set a variable to this** in cases when you whant to say that something doesn't exist (equal to nothing).

**Boolean**
```true``` or ```false```

**Number**

*Floating point* number (there's always some desimals). There is only one 'number' type and it can make math weird.

**String** - a sequence of characters ('' and "" can be used). Double quotes can be used to specify that we're dealing with a string.

**Symbol** - used in ES6. It's not fully supported by all browsers.

*"The Symbol type allows us to obtain values that cannot be re-created, that is, they are unique and immutable identifiers."*

```javascript
  Symbol() === Symbol() // false
```

```javascript
  const a = Symbol('a');
  const otherA = Symbol('a');
  a === otherA // false
```

(Link to article) [https://latteandcode.medium.com/javascript-do-you-know-the-symbol-type-9dfbf40b6eef]

## Operators

**Operator**: special function that is syntactically (written) differently. Kind of special type of functions. Generally, operators take two parameters and return one result.

**Infix notation** means that the function name, the operator, sits between the two parameters.

```javascript
  3 + 5 // infix
  +3    // prefix
  3+    // postfix
```

## Operator Precedence and Associativity

**Operator Precedence**: which operator function gets called first. Finctions are called in order of precedence. The higher precedence wins.

**Associativity**: what order operator functions get called in: left-toright or right-to-left when functions have the same precedence.

(Table operators precedence and associativity in JS) [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence]

```javascript
  var a = 3 + 4 * 5;    // = 23
```
Order of exeqution: ```*``` --> ```+``` --> ```=```

```javascript
  var a = 2, b = 3, c = 4;

  a = b = c;    // associativity of '=' right-to-left

  console.log(a); // 4
  console.log(b); // 4
  console.log(c); // 4
```
```javascript
  var a = (3 + 4) * 5;    // = 35 because grouping goes first
```

## COERCION

**Coercion**: converting a value from one type to another. This happens quite often in JS because it's dynamicaly typed.

```javascrit
var a = 1 + '2'; // => '12'
```
First parameter 1 was coerced by the JS engine in to a string.

### Some examples

```javascript
  Number(true) // =>  1
  Number(false) // =>  0
  Number(undefined) // =>  NaN (not a number)
  Number('3') // => 3
  Number(null) // => 0
```


## Comparison operators

```<``` - has the left-to-right assotiativity

```javascript
console.log(1 < 2 < 3); // => true
```
Because ```1 < 2  => true```. ```true``` coercing to ```1```
```javascript
  Number(true) // =>  1
```
and comparing with ```3```. ```1 < 3 => true```.

```javascript
console.log(3 < 2 < 1); // => true ( )
```

Because ```3 < 2  => false```. ```false``` coercing to ```0```
```javascript
  Number(false) // =>  0
```
and comparing with ```3```. ```0 < 1 // => true```.

### Equality operator ```==```

```javascript
  3 == 3 // => true
  "3" == 3  // => true , because of coercion
  false == 0 // true

  var a = false;
  a == 0;  // => true

  null == 0;  // => false

  null < 1;  // => true

  "" == 0; // => true

  "" == false // => true
```
This is actually considered a negative part of the language in comparison operators, especially double equals causes strange errors because of unexpected ways in which it behaves.

Double equals using an empty string and zero, that's true.

This problems solves with ```===``` (strict equality) and save your life ))
**Strict equality** compares two things, but doesn't try to coerce the values.
If the two values are not the same type, it just return ```false```.

```javascript
  3 === 3 // => true
  '3' === '3' // => true
  '3' === 3   // => false
```

Using the triple equals will prevent us from having some odd potential errors in our code.

In general, try to do comparison against things in your code that you know will be the same type.

**Use ```===/!==``` in 99% of the time when making equality comparisons.**

**Don't use ```==/!=``` unless you explicitly, unless you consciously want to coerce the two values.**

(Equality Comparisons Table) [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness]


## Object.is()

The ```Object.is()``` method determines whether two values are the same value.
(link) [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is]


## Existence and Booleans

```javascript
  Boolean(undefined) // => false
  Boolean(null)   // => false
  Boolean("")     // => false
  Boolean(0)     // => false
```

```javascript
  var a;

  // some code when we set value to the a or not set

  if (a) {  // just checking some value is set
    console.log('Something is there.');
  }

```

## Default values

```javascript
  function greet(name) {
    console.log('Hello ' + name);
  }
  greet();  // => Hello undefined
```
Good practice - use default value.

```javascript
  function greet(name = '<You name here>') {  // in ES6
    name = name || '<You name here>';   // before ES6
    console.log('Hello ' + name);
  }
  greet();  // => Hello <You name here>
```

### || / or operator

```javascript
  false || true     // => true
  undefined || 'hello'    // => 'hello'
  0 || 1    // => 1
```
```||``` operator returns first value which can coerse to ```true```


## Framework aside: Default values

```html
  <html>
    <head> </head>
    <body>
        <script src="lib1.js"></script>
        <script src="lib2.js"></script>
        <script src="app.js"></script>
    </body>
  </html>
```
```javascript
  // lib1
  var libraryName = 'Lib1'
```
```javascript
  // lib2
  var libraryName = 'Lib2'
```
```javascript
  // app
  console.log(libraryName);   // => Lib2
```
These three script tags are not creating new execution context. They're not separating the code in any way. Quite literally, they're stacking the code on top of each other. And then running all of this JS as if it was inside a single file.

Best to do:
```javascript
  // lib2
  window.libraryName = window.libraryName || 'Lib2';
  console.log(window.libraryName) // => Lib1
```
