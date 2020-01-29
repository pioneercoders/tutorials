<p> In JavaScript, there's many different ways for declaring the functions.</p>

<h4> different ways of declaring functions </h4>
@CODE_START@@HTML@function A(){};             // function declaration
var B = function(){};       // function expression
var C = (function(){});     // function expression with grouping operators
var D = function foo(){};   // named function expression
var E = (function(){        // IIFE that returns a function
  return function(){}
})();
var F = new Function();     // Function constructor
var G = new function(){};   // special case: object constructor
var H = x => x * 2;         // ES6 arrow function
}@CODE_END@

<h3> Function declarations </h3>
<p> Function declarations are probably the most familiar and oldest way of doing things in JavaScript.</p>

@CODE_START@@HTML@function add(x,y){
  return x+ y;
};
var sum = add(10,20);
console.log("sum ::", sum);@CODE_END@

<h3> Function expressions</h3>
<p> A function expression looks similar to function declarations, except that the function is assigned to a variable name. </p>

@CODE_START@@HTML@var add = function(x,y){
  return x+ y;
};
var sum = add(10,20);
console.log("sum ::", sum);@CODE_END@

<h3> Function expressions with grouping operators </h3>
@CODE_START@@HTML@var add = (function(x,y){
  return x+ y;
});
var sum = add(10,20);
console.log("sum ::", sum);@CODE_END@

<h3> Named function expression</h3>
<p> Here we have our same old friend, the function expression. But instead of assigning the variable to an anonymous function, we’re assigning it to a named function. function’s name is accessible in the function itself, this turns out to be useful for recursive functions, much more useful than the plain old anonymous function.</p>
@CODE_START@@HTML@var countdown = function a(count){
  if(count > 0) {
    count--;
    return a(count);  // we can also do this: a(--count), which is less clear
  }
  console.log('end of recursive function');
}
countdown(5);@CODE_END@

<h3> Immediately-invoked function expressions</h3>
<p> "Execute this function, whose return value is another function, and assign that to the variable E". This may seem like magic, but it’s actually quite simple, and the pattern is powerful and has useful applications, the most famous of which is the module pattern. </p>

@CODE_START@@HTML@var E = (function(){
  return function(){
	console.log('function form inner..')
  };
})();@CODE_END@

<h3> Function constructor </h3>
<p> This method is extremely old and it’s not recommended to be used. You pass in an unlimited number of arguments in the front, then the actual function body appears as a string in the last argument (because it’s a string, it’s effectively the equivalent of eval(), and isn’t recommended).</p>

@CODE_START@@HTML@var F = new Function('arg1', 'arg2', 'console.log(arg1 + ", " + arg2)');
F('foo', 'bar');  // 'foo, bar'
@CODE_END@

<h3> Special case - object constructor </h3>
<p> var G = new function foo(){}; </p>
<p> new function(){}; creates a new object and invokes the anonymous function as its constructor. If an object is returned from the function, that becomes the resulting object, otherwise a new object is created from scratch and function is executed in the context of that new function </p>

@CODE_START@@HTML@var Person = function(){
  console.log(this);  // Person
}
var joe = new Person();
@CODE_END@
<h3>Arrow functions </h3>
