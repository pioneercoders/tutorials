<h4>What is default parameters?</h4>
<p>We can assign default values to function paramaters, which is used when caller not provide the parameter value .
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
<p>

```javascript
/**
 * Default parameter values allow you to initialize parameters if they were not explicitly supplied.
 * This means that you no longer have to do options = options || {};
 */

// ES5
function testFunc(x, y, z) {
    if (y === undefined)
        y = 7;
    if (z === undefined)
        z = 42;
    return x + y + z;
}
console.log(testFunc(1));

// ES6
function testFunc(x, y = 7, z = 42) {
    return x + y + z;
}
console.log(testFunc(1));
```