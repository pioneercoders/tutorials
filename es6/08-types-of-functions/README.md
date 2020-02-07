<h4>What are the function types are available?</h4>
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

<h4>Function Declarations/Named function</h4>

```javascript
function add(x,y) {

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


