<details open>
<summary open>Write a program to assign a function to variable.</summary>
<p>

```javascript
var add = function(x,y) {
    let sum = x + y;
    return sum;
}
var result = add(10,30);
console.log(result);
```

</p>
</details> 

<details >
<summary open>Write a program to pass a function to another function as argument.</summary>
<p>

```javascript
 function f1(fun, x, y){
  let result = fun(x,y);
  return result;
 }
var add = function(x,y) {
    let sum = x + y;
    return sum;
}
var sub = function(x,y) {
    let sum = x - y;
    return sum;
}
var result = f1(add, 4, 5);
console.log(result);
var result1 = f1(sub, 9, 2);
console.log(result1);
```

</p>
</details> 
