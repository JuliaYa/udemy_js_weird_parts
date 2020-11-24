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
