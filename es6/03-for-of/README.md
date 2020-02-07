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
