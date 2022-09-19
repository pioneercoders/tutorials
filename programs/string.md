
### Why we need data types?  
To capture the data from user and based on that data to compute the logic.  
### What is data types?  
Data type is used to define the type of the data we are capturing like integers, string and boolean types of data.  
### What are the data types are there in java?  
Int, Boolean, String, Char etc.  

### Sample Programs
<details>
<summary>Print Hellow World Program.</summary>
<p>

```java
class App{  
    public static void main(String args[]){  
     System.out.println("Hello Java");  
    }  
}  
```

</p>
</details> 

<details>
<summary>Print Welcome to PC Program.</summary>
<p>

```java
class App{  
    public static void main(String args[]){  
     System.out.print("Welcome to PC.");  
    }  
}  
```

</p>
</details> 




<h3>What is Scope?</h3>
<p>"scope" refers to where a variable is accessible, based on where and how the variable was declared. </p>
<p>Global variables have, unsurprisingly, global scope - they can be accessed (set or read) anywhere in your script.</p>
<p>Variables defined with the var keyword in function have "function scope" that is more limited; these are variables that might be accessed only within a function (often the function in which they are defined).</p>

```javascript
var pi = 3.45;
p = 3;
function area(r) {
	var a =  pi * r * r;
	area = a;
	return a;
}
var ar = area(3);
console.log("area of circle from variable ar", ar);
console.log("variable area value outside function", area);

for(var x=0;x<2;x++){
}
console.log("X value outside for loop:"+x);
```

<p>the fact that the var keyword ensures that a variable created inside of a function is local to that function</p>
<p> The let keyword works in a similar fashion but has block-level scope - with for loops and if statements being two common examples of enclosing blocks.</p>

<h4> Understanding let and const in JavaScript ES6</h4>

<p>The first thing to understand about let and const is that they are block scoped, compared to var, which is function scoped. This means they are local to the closest block (curly braces) that they are defined in, whereas var is local to the entire function, or even global if defined outside functions.</p> 
<p>The difference between let and const lies in that the former should be used to hold variables that are subject to change, while const, as the name implies, data that you know will stay constant. In fact, trying to reset a const's value after it's been set will result in an error.</p>

```javascript
const pi = 3.45;
function area(r) {
	var a =  pi * r * r;
	return a;
}
var ar = area(3);
console.log("area of circle from variable ar", ar);

for(let x=0;x<2;x++){

}
//we cant access x outside of the loop.
//console.log("X value outside for loop:"+x); 
```
