## Execution Contexts and Lexical Environments

**Sintax parser**: a program that reads your code and determines what it does and if its grammar is valid. 

Your code                           Computer Instruction
                        ------>
function Hello() {                      translation +
    var str = 'Str';                    other stuff
}      

**Lexical environment**: where something sits phisically in the code you write

 In most popular PL the lexical environment is important, that means that where you see things written gives you an idea of where it will actually sit in the computer's memory. And how it will interact with other variables, functions and elemtnts of a program. Thats because compiler cares about where you put things.
 **When we talk about LE of something in the code we're talking about where it's written and what surrounds it.**
 
 **Execution context**: a wrapper to help manage the code that is running

 Thare are lots of LE. Which one is running is managed via EC. It can contain things beyond what you've written in your code. Cuz our code can be processed a whole other set of programs that someone else wrote.

 ## Conceptual Aside: Name/Value Pairs and Objects

**Objects in JS are incredibly important.**
What we need to properly understand objects in JS:
 
  **Name/Value pair** is a name which maps to a unique value. The name may be defined more than once, but only can have one value in any given context. That value may be more name/value pairs.

  **Object**: a collection of name value pairs. The simplest definition when talking about JS but not for all PL.
  ```
  var Adress = {
      street: 'Toreza',
      building: 95,
      apartment: {
          number: 221,
          floor: 13
      }
  } 
  ``` 

## The Global Environment and The Global Object
JS engine is creating **Global Object** and **this** every time.
GO in browsers is the Window.
Each window(tab) has its own EC and its own global EC.
On global level in browsers GO(window) = this.

Global in JS means "Not inside a Function", that means code or variables that aren't inside a function is global.