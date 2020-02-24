<h4> What is Closures Function? </h4>
<p>In Javascript we can write a function inside other function that we call it as innerfunctions. A closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
in another words a closure is an inner function that has access to the outer (enclosing) function's variables, paramaters and global variables. </p>

```javascript
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
let val = count();
console.log(val);
```
<p>In above example, say is inner function which is able to access outer function variable text. </p>
<p>Closures have access to the outer function’s variable even after the outer function returns</p>  


```javascript
userService = (function () {
    var doLogin = function () {
        alert('hello');
        // do some critial logic like encript pwd and other stuff.
    }

    return {
        login : function () {
            doLogin();
        }
    }
})();
userService.login();
```
<p>As you can see there, a is now an object, with a method login ( userService.login() ) which calls doLogin, which only exists inside the closure. You can NOT call doLogin directly.</p>

<h6>Recommended to gothrough below tutorials also to get more knowledge.</h6>
<a href="https://javascript.info/closure" target="_blank"> Referral Lexical Environment more in detailed.</a>  <br>
<a href="https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36" target="_blank">More detailed interview point of view.</a>
