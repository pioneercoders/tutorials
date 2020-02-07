<h4> What is Arrow Function? </h4>
<p>An arrow function expression has a shorter syntax than a function expression and does not have its own this, arguments, super, or new.target. </p>

```javascript
var names = ['Ram', 'Krishna', 'Ravi'];
names.map((name) => {
	 console.log(name)
	});
	
var add = (x,y) =>  x + y;
var sum = add(2,4);
console.log("sum of 2+4 = " sum);
```
<h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>

### Arrows
Arrows are a function shorthand using the `=>` syntax.  They are syntactically similar to the related feature in C#, Java 8 and CoffeeScript.  They support both statement block bodies as well as expression bodies which return the value of the expression.  Unlike functions, arrows share the same lexical `this` as their surrounding code.

```JavaScript
// Expression bodies 
var odds = evens.map(v => v + 1);
var nums = evens.map((v, i) => v + i);
var pairs = evens.map(v => ({even: v, odd: v + 1}));

// Statement bodies
nums.forEach(v => {
  if (v % 5 === 0)
    fives.push(v);
});

// Lexical this  
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
}
```

More info: [MDN Arrow Functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
```JavaScript
 How it works?

// this function
var func = function (param) {
    return param.split(" ");
};

// would become:
var func = param => param.split(" ");

// Examples
var users = [
    {name: 'Jack', age: 21},
    {name: 'Ben', age: 23},
    {name: 'Adam', age: 22}
];

// ES5
var ages = console.log(users.map(function (user) {
    return user.age;
}));   // [21, 23, 22]

// ES6
var ages = users.map(user => user.age);
console.log(ages);  // [21, 23, 22]

// Because reduce takes two parameters, brackets are required
// to make it clear that the parameters are for the arrow function, not for the reduce call.
var sum = ages.reduce((a, b) => a + b);
console.log(sum);   // 66

// IIFE
(x => x * 2)(3); // 6

// Scope
// In ES5
document.body.addEventListener('click', function (evt) {
    console.log(evt, this); // EventObject, BodyElement
});

// In ES6
document.body.addEventListener('click', evt=>console.log(evt, this)); // EventObject, BodyElement
```
