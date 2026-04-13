<!-- ep-1 -->

Everything in javascript happens inside the Execution context

Execution context - you can assume it as a big box or container in which whole js code is executed

It has 2 components  in it ->

1. memory component (variable environment) - contains variables and functions as the key value pairs eg. a : 10 , fn:{} whole function

2. code component (thread of execution) - this is the place where whole js code is executed one line at a time 
   
javascript is the synchronous single-threaded language. 


<!-- ep-2 -->

what happens when you run javascript code ?

execution context is created in two phases

1 - memory creation.
2 - code execution.

memory creation phase: in this js will allocate memory to all variables and functions, it stores a special value known as undefined. 

code execution phase: in this we'll see how the code is executed after the memory creation phase in this js runs again the whole js program line by line and it executes the code now
till now the values were undefined but now they will get replaced by their original values.

when you run a function or u invoke a function it creates a brand new execution context inside this  is created  and again  it will have the memory component and a code component  now we will go through the creation of execution  context and again their will be two phases(memory,code) and so on....

one more thing that happens when whole function is executed is that this whole execution context for that instance of that function will be deleted the  value will be saved in memory replacing undefined. and the control moves to next line.


but all this is too much to handel for js engine execution context is created one by one  inside and inside and it is very tough to manage  but it does it very beautifully it handel everything -  execution context, creation ,  deletion  and the control
 it manages through the stack it has its own stack called callstack

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

during the creation phase the js engine moves the functions and variables to the top of the code is called hoisting. 

or 

Hoisting is a JavaScript behavior where variable and function declarations are moved to the top of their scope during the creation phase, before the code executes.

 <!--ep-4  -->

 whenever you create a global object a this is created  even for the functional execution context and for thr global execution context.

 js is not just run on browsers it is also run on servers and on many others devices and places  and where ever js is running their must be a js engine. just like in chrome it is v8 , safari has its own, internet explorer has it own etc so all this js engine has a responsibility to create this global object. in case of browsers it is known as window in case of node it is known as something else , wherever u run thr js program it is different but their is always a global object created. even though  our file is empty js engine will create this global object and  At this global level or the base level in the global execution context 

this is === to window object is true
(this === window)


<!-- scope and lexical environment  -->

scope means where you can access specific variable or a function in your code their can be multiple types of scopes eg. global scope , block scope , functional scope etc

function abcd(){
                     (function scope)
}

{
    (block scope)
}

var a = 5 ( global scope ) 

var is a functional scope but let and const are block scope

<!-- variable shadowing -->

for eg.

function test(){
let a = "hello";

if(true){
    let a = "hi";
    console.log(a)
}
console.log(a)
}
test()

output-

hi
hello


Variable Shadowing means when a variable declared inside a smaller scope (like a function or block) has the same name as a variable in an outer scope, so the inner variable hides or “shadows” the outer one. Inside that scope, JavaScript will use the inner variable instead of the outer variable. But the outer variable still exists outside that scope.

Example idea:
If there is let a = 10 outside and inside a block you write let a = 20, then inside that block a will be 20, because the inner a shadows the outer a.

but it should not cross the boundary of scope that is we can shadow var variable using let but not the vice versa.
 but if we do it will be known as illegal shadowing and will give that variable is it already defined.

 <!-- declaration -->

 let and const cannot be redeclared in the same scope but var can be.

<!-- initialization -->
 var and let can be declared without the initialization but const cannot.

 <!-- re-initialization -->

 var and let can be updated  but  const can never be. 

 <!-- temporal dead zone -->

 time between the declaration and the initialization of let and const variables.

 let and const are also  hoisted but in temporal dead zone 

eg.

function abc(){
    console.log(a,b,c);

    const c = 30;
    let b = 20;
    var c = 10; 
}
abc();


in this var is hoisted but let and const are also hoisted but in temporal dead zone  and reference error will be seen 

temporal dead zone is the term to describe the state where variables are in the scope but not yet declared 


<!-- closures -->

function along with its lexical scope forms a closure  

<!-- hof -->

higher order function  is a function in which  it takes another function to its input to itself or returns a function from itself .

a function passed into hof is known as callback function  this is because of functions are first class citizens in js 

<!-- callback functions -->

A callback function is a function that is passed as an argument to another function and is executed later.
or
in which you can take a function and pass it to another function. 

JavaScript is a synchronous and single-threaded language, but with the help of callbacks, we can perform asynchronous tasks.

Callback functions are very powerful in JavaScript because they help us handle asynchronous operations like:
- setTimeout
- API calls
- event handling



eg. -> 

function x(y){

}
x( function y(){

})

in this we have called function x and passed another function y in it . y over here is the callback function and u have passed y inside x that means now whenever x wants it can call y anytime in the code  thats the reason its a callback func.

<!-- garbage collection & removeEventlisteners -->

JavaScript uses garbage collection to automatically remove unused memory. It deletes objects that are no longer reachable.

But in the case of event listeners, memory is not freed easily.
Whenever we attach an event listener, it creates a closure (it remembers its surrounding variables).

Even if the call stack is empty, the memory is not released because:
-> JavaScript doesn’t know when the user might trigger the event (like a click)
-> So it keeps the function and its closure in memory

This can lead to memory leaks and slow performance if we don’t remove unused listeners.

That’s why we use removeEventListener to remove the event and allow garbage collection to free memory.

<!-- Event loops & Callback queue -->

event loop has only one work to monitor the call stack and the callback queue. so when it sees that callstack is empty it checks in call back queue it takes the function waiting their to the call stack and from their its quickly executed.

The callback queue or(tasks queue) is a waiting line where callback functions from asynchronous tasks (like setTimeout, API calls, or events) are stored. Since JavaScript can do only one thing at a time, these callbacks wait in the queue until the call stack becomes empty, and then JavaScript executes them

<!-- microtask queue  -->

The microtask queue is a special, high-priority queue where callbacks from Promises (like .then() and .catch()) are stored. These tasks are executed before the normal callback queue as soon as the call stack becomes empty, so they run faster than other async callbacks.
(promises and mutation observer)

-->> starvation of the functions in callback queue -  Callbacks in the normal callback queue don’t get a chance to run because the microtask queue (Promises) keeps getting executed again and again.



<!-- callback hell -->

callbacks are superpowerfull way of  handeling async operatins in javascript . infact asychronous js exist because callback exists.

-> while we are writing call back we face many issues-

1. callback hell : the callback inside callback a lott of nested callbacks. the code becomes unmaintainable
2. inversion of control : that we loose the control of our program bcoz we pass the callback fnc  into another fnc and now we have given the control of our function to some other function . and now we dont know that whether that function will ever execute our callback or not so this is another big isssue with callback

