<h4>What is for of? </h4>
The for...of statement creates a loop iterating over iterable objects, including: built-in String, Array, array-like objects.

```javascript
var productList = [{"skuid":"p123","name":"Iphone"}, {"skuid":"p345","name":"S3"}];
for(let product of productList) {
  console.log(product);
}
```
<h4> What is the issue with forloop/for in ?</h4>
<p><b>for in </b>: The for...in statement iterates over all enumerable properties of an object.

```javascript
  let product = {"skuid":"p123","name":"Iphone"};
  for(const property in product) {
    console.log(`${property}: ${product[property]}`);
  }
```
</p>
<p>
<b>for loop:</b> More flexable for iteration in forward , backward and as we want.

```javascript
  let productSkuIds = [3 , 6, 2, 56, 78, 90];
  for(var i =0; i < productSkuIds.length; i = i+3) {
    console.log(productSkuIds[i]);
  }
``` 
</p>

<p>

```javascript
/**
 * New for-of loop for looping over iterable objects
 */


// Conveniently iterate over data in Arrays, Sets, and Maps:
// ES6
for (let word of ["one", "two", "three"]) {
    console.log(word);
}

let s = new Set([3, 4, 5]);
for (let value of s) {
    console.log(value);
}

let m = new Map([['red', 'rojo'], ['blue', 'azul']]);
for (let [name, value] of m) {
    console.log(name + " = " + value);
}

// The for-of and for-in loops look similar, but they do two very different things.
// - for-in is for inspecting object properties. It works on any object, and it always loops over the names of the object's enumerable properties.
// - for-of is for looping over data. It only works on iterable objects. ie. objects with a suitable [iterator] method.

var colors = new Set(['rojo', 'amarillo', 'azul']);
colors.language = 'es';     // add an expando property (ie. JS objects allow you to write a new property to an object without having needed to predefine that property.ß)

for (let name in colors) {
    console.log(name);      // "language" (the property name)
}

for (let word of colors) {
    console.log(word);      // "rojo", "amarillo", "azul" (the data)
}
```

</p>