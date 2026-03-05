<!-- ep-1 -->

Everything in javascript happens inside the Execution context

Execution context - you can assume it as a big box or container in which whole js code is executed

It has 2 components  in it ->

1 memory component (variable environment) - contains variables and functions as the key value pairs eg. a : 10 , fn:{} whole function

2 code component (thread of execution) - this is the place where whole js code is executed one line at a time 
   
javascript is the synchronous single-threaded language. 



<!-- ep-2 -->

what happens when you run javascript code ?

execution context is created in two phases

1 - memory creation.
2 - code execution.

memory creation phase: in this js will allocate memory to all variables and functions, it stores a special value known as undefined. 

code execution phase: in this we'll see how the code is executed after the memory creation phase in this js runs again the whole js programs line by line and it executes the code now
till now the values were undefined but now they will get replaced by their original values.

when you run a function or u invoke a function it creates a brand new execution context inside this  is created  and again  it will have the memory component and a code component  now we will go through the creation of execution  context and again their will be two phases(memory,code) and so on....

one more thing that happens when whole function is executed is that this whole execution context for that instance of that function will be deleted the  value will be saved in memory replacing undefined. and the control moves to next line.


but all this is too much to handel for js engine execution context is created one by one  inside and inside and it very tough to manage  but it does it very beautifully it handel everything execution context creation deletion  and the control it manages the stack it has its own stack called callstack

in this callstack every time in the bottom of the stack we have our global execution context.  that means whenever any js program is run this call stack is populated with the global execution context. the whole execution context is pushed inside the stack. and whenever a function is invoked a new execution context is created then it move to the stack  then whole fnc will be executed it will also pop out from the stack and the control goes back to global execution context. 

this callstack is only for managing the execution context. so whenever execution context is created it moves  into the stack and when the execution context is deleted it move out of the stack 

and the the end the execution and call stack both gets empty and we are done with our program.
this is how whole code inside the  js engine is executed

callstack maintains the order of execution of execution contexts.

call stack also known as - 

1 execution context stack 
2 program stack
3 control stack
4 runtime stack
5 machine stack

<!-- ep-3  -->

hoisting - it is a phenomenon in js by which you can access  the variables and functions even before you initialized it or put some value to it  and access it without any error.

or 

Hoisting is a JavaScript behavior where variable and function declarations are moved to the top of their scope during the creation phase, before the code executes.

