## Execution Contexts and Lexical Environments

**Syntax parser**: a program that reads your code and determines what it does and whether its grammar is valid. 

| Your code | Computer Instruction |
| ----------| -------------------- |
| ` function Hello() {     var str = 'Str'; } `; | translation + other stuff |

**Lexical environment**: where something sits phisically in the code you write

 In most popular PL the lexical environment is important, that means that where you see things written gives you an idea of where it will actually sit in the computer's memory. And how it will interact with other variables, functions and elemtnts of a program. Thats because compiler cares about where you put things.
 **When we talk about LE of something in the code we're talking about where it's written and what surrounds it.**
 
 **Execution context**: a wrapper to help manage the code that is running

 Thare are lots of LE. Which one is running is managed via EC. It can contain things beyond what you've written in your code. Cuz our code can be processed a whole other set of programs that someone else wrote.

 ## Conceptual Aside: Name/Value Pairs and Objects

**Objects in JS are incredibly important.**
What we need to properly understand objects in JS:
 
  *Name/Value pair* is a name which maps to a unique value. The name may be defined more than once, but only can have one value in any given context. That value may be more name/value pairs.

  *Object* is a collection of name value pairs. The simplest definition when talking about JS but not for all PL.
  ```javascript
  var Address = {
      street: 'Toreza',
      building: 95,
      apartment: {
          number: 221,
          floor: 13
      }
  } 
  ``` 

## The Global Environment and The Global Object
JS engine is creating **Global Object** and `this` every time.
GO in browsers is the Window.
Each window(tab) has its own EC and its own global EC.
On global level in browsers GO(window) = this.

Global in JS means "Not inside a Function", that means code or variables that aren't inside a function is global.

## The execution context: creation and "hoisting"

```javascript
b();    // Called b!
console.log(a); // undefined

var a = 'Hello World!';

function b() {
    console.log('Called b!');
}

b();    // Called b!
console.log(a); // Hello World!
```

### Creation phase

Global Object       this            Outer Environment

Setup memory space for variables and functions
                "**HOISTING**"

This means is that before your code begins to be executed line by line the JS engine has already set aside memory space for the variables and functions that you've created in that entire code. So when the code begins to execute line by line, it can access them.

Функции попадают в память целиком, а вот для переменных выделяется место, но значение не присваивается и если написать код с использованием переменной до того как ей присвоено значение он сработает, но значение будет "**undefined**". Если использовать переменную без обьявления, получим ошибку.

### Execution phase

A moment where it actually executes your code line by line, that's when these kind of assigments are set, where variables equals something.
All variables in JS are initially set to undefined, and functions are sitting in memory in their entirety.
That's why it's a bad idea to rely on hoisting in any way.
Just use variables and functions after declaration.

The fact is that what I wrote is not what's directly being executed but the JS engine is taking my code and making decisions.

## JavaScript and 'undefined'

`undefined` and error 'a is not defined' not the same thing.

`undefined` is a special value/keyword that JS init internally. It means that variable hasn't been set.

```javascript
var a;
console.log(a);     // undefned

if(a === undefined) {
  console.log('a is undefined!'); // a is undefined!
} else {
  console.log('a is defined!);
}
```

```javascript
console.log(a);     

// uncaught ReferenceError: a is not defined (don't have it in memory)
// and app will stop

if(a === undefined) {
  console.log('a is undefined!'); // a is undefined!
} else {
  console.log('a is defined!);
}
```
### Never do that!
```javascript
a = udefined;
```
It can be hard with debugging later.

Alternative meaning for **'underfined'** - **I've never set this value**

## The execution context: code execution

### Execution phase

Global Object this Outer Environment Runs Your Code

```javascript
function b() {
  console.log('Called b!');
}
b(); // Called b!

console.log(a); // underfined
var a = 'Hello World!';
console.log(a); // Hello World!

```

## Single threaded, synchronous execution

**Single threaded**: one command at a time.
JS behaves in a single threaded manner.

Synchronous: one in a time. And in order.

In JS only one thing is happening at the time.

## Function invocation and the execution stack

Invocation: running a function

In JS, by using parenthesis ()

```javascript
function b() {}

function a() {
  b();
}

a();
```

### Execution Stack
```
b() EC

a() EC
```

Global Execution Context

Every time when function was called a new execution context is created for that function. The variables within it are set up during the creation phase.

## Functions, context and variable enviroments

**Variable environment**: where the variables live and how they relate to each other in memory.

```javascript
function b() {
 var myVar;
 console.log(myVar); // undefined
}

function a() {
 var myVar = 2;
 console.log(myVar); // 2
 b();    // undefined
}

var myVar = 1;
console.log(myVar); // 1
a();
console.log(myVar); // 1
```

### Execution Stack

        b() EC
    (myVar undefined)

        a() EC
    (myVar 2)

Global Execution Context 
    (myVar 1)


**Scope**: where we are able to see the variable.

```javascript
function b() {
 console.log(myVar); // 1 (from Global EC)
}

function a() {
 var myVar = 2;
 console.log(myVar); // 2
 b();    // 1
}

var myVar = 1;
console.log(myVar); // 1
a();
```

## Scope, ES6, and let

**Scope**: where a variable is available in your code and if it's truly the same variable, or a new copy

ES6 or ECMAScript 2015 is introdusing a new way of declaring variables.

**"let"** allows the JS engine to use block scoping.

During the creation phase it still plased in memory and set to undefined, however you not allowed to use it until the line of code is run during the execution phase that actually declares the variable.

```javascript
if (a > b) {
 console.log(c);
 let c = true;
}
```

### First

If you tried to use ***c*** in this example before the ```let c = true```, you'd get an error "Cannot access 'c before initialization". It's still in memory but the engine just won't allow it.

### Second

Then let variable declared inside the block ```{...}```, it's only avalable inside that block at that period of time for the running code.

If you have a loop and are running the same code over and over but you have a let statement, you'll actually get a different variable in memory each time the loop is running.
