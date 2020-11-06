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



