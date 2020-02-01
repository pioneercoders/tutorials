<h4> What is Closures Function? </h4>
<p>In Javascript we can write a function in another function that we call as innerfunctions.
A closure is an inner function that has access to the outer (enclosing) function's variables, paramaters and global variables. </p>

```javascript
function sayHello(name) {
var text = 'Hello ' + name;
var say = function() { 
	console.log(text); 
	  }
	  say();
	}
sayHello('Krishna');
```
<h3>Please open the console and see the log </h3>

<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>

```html
<iframe id="preview"></iframe>
```
<p>In above example, say is inner function which is able to access outer function variable text. </p>
<p>Closures have access to the outer function’s variable even after the outer function returns</p>
