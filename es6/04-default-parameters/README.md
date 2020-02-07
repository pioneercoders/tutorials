<h4>What is default parameters?</h4>
<p>We can assign default values to function paramters, which is used as default value when function caller missed passing parameter value . 
</p>

```javascript
function add(x,y) {
  return x + y;
}
var result = add();
var result1 = add(10);
var result2 = add(10,20);
console.log(result);
output: 
0
10
30
```

<h4>What happen with out default parameters?</h4>

```javascript
function add(x,y) {
  return x + y;
}
var result = add();
var result1 = add(10);
var result2 = add(10,20);
console.log(result);
output: 
undefined
undefined
30
```
