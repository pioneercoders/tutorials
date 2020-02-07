<h4>What is template string? </h4>
Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them. Template literals are enclosed by the backtick (` `) (grave accent) character instead of double or single quotes.

```javascript
var users = ["Krishna", "Siva", "Ramu"];
let isM = true;
for(var i = 0; i < users.length; i++) {
    var welcomeMessage = `Welcome to Pioneer Coders ${ isM ? "Mr." : "Mis." }${userName}`; //variable interpolation
    console.log(userName);
}

let email = "info@pioneercoders.com";
let mobile = "12345567";
let url = `http://pioneercoders/user/get?email=${email}&mobile=${mobile}`;
console.log(url);
```

<h4>Why we need template string? </h4>
Before we used to see strings between single ‘ ’ or double “ ” quotes , as shown below :

```javascript
var name = "Krishna" ;
var hello = "Hello "+ name ;
console.log(hello); //Hello Krishna
```