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
