<h4>What are the types of functions available?</h4>
<ul>
    <li>Function Declarations/Named function</li>
    <li>Function Expressions</li>
    <li>Anonymous function</li>
    <li>Call back function</li>
    <li>Closer Function</li>
    <li>Higher order functions</li>
    <li>Function constructor</li>
    <li>Arrow Function</li>
    <li>Promise Function</li>
    <li>Generator Function</li>
</ul>

<h4>What is function?</h4>
A function is a block of code which deals with some specific funcanality defined once and called once/multiple times later. Generally functions will take input, do business logic/computational logc and return output. Input and output are optional.

```javascript
// function defination syntax.
function function_name( arguments/inputs ) {
    // set of statements to do some logic.
    return output; // optional
}
// function calling.
take out put value in to varialbe if present = function_name(provide input values);
```
<h4> Why do we need functions?</h4>
We can avoid the code redundancy, we need not to write same set of line multiple times.

<h4>Function Declarations/Named function</h4>
Defining A function with function keyword, followed by an obligatory function name, a list of parameters in a pair of parenthesis and block of code is called function declaration.

```javascript
function add(x,y) {
    return x + y;
}
var result = add(20,30);
console.log(result);
```
<h4>What is a Function Expression?</h4>
A function can be stored/assigned to a variable:

```javascript
var mul = function (a, b) {return a * b};
var result = mul(10,20);
console.log(result);
```

After a function expression has been stored in a variable, the variable can be used as a function. Functions stored in variables do not need function names. They are always invoked (called) using the variable name.

<h4>Anonymous Functions</h4>
function with of name we call it as anonymous function.  
There are three main anonymous function declarations you will run into:  

<h6> IIFE (Immediately Invoked Function Expression) </h6>

```javascript
( function (x) { 
    return x * 2; 
    } )(2);
```
<h6>Assignment to Variable</h6>

```javascript
var multiplyByTwo = function (x) { 
    return x * 2; 
};
```

<h6>Anonymous Functions used as a parameter passed to another function</h6>

```javascript
[1, 2, 3, 4, 5].map( function(x) { 
    return x * 2;
    } );
```


