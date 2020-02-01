<h4>1.Write a program to print elements in array?</h4>

```javascript
var array = [3 , 6, 2, 56];

for (i=0; i<array.length;i++){
    
    console.log(array[i]);
  
}
```
Output:
3  
6  
2  
56  

<h4>2.Write a program to print largest Number in array?</h4>

```javascript
var array = [3 , 6, 2, 56, 32, 5, 89, 32];
var largest= 0;

for (i=0; i<=largest;i++){
	if (array[i]>largest) {
		var largest=array[i];
	}
}
console.log(largest);
```
Output:
89  

<h4>3.Write a program to print Least Number in array?</h4>
```javascript
var array = [3 , 6, 2, 56, 32, 5, 89, 32];
var min = array[0];
for (var i = 1; i < array.length; i++) {
    if (min > array[i])
        min = array[i];
}

console.log(min);
```

Output:
2  
<h4>4.Write a program to print duplicate element in array?</h4>

```javascript
var oldArray = [3 , 6, 2, 56, 32, 5, 89, 32];
for (var i = 0; i < oldArray.length; i++) {
     for (var j = i + 1 ; j < oldArray.length; j++) {
          if (oldArray[i]==oldArray[j]) {
               // got the duplicate element
                console.log(oldArray[i]);
        }
    }
}
```

Output:
32  
