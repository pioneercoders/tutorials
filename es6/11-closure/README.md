<h4> What is Closures Function? </h4>
<p>In Javascript we can write a function inside other function that we call it as innerfunctions. A closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
in another words a closure is an inner function that has access to the outer (enclosing) function's variables, paramaters and global variables. </p>

```javascript
function getIncrementCounterFun() {
  let count = 0;

  return function() {
    console.log(count++);
  };
}

let incFun = makeCounter();
incFun();
```
<p>In above example, say is inner function which is able to access outer function variable text. </p>
<p>Closures have access to the outer function’s variable even after the outer function returns</p>  
[Referial Link](https://javascript.info/closure)
