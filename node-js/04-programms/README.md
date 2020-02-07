
<details>
  <summary>1.Write a program to print elements in array?</summary>
	<p>
 
 ```javascript
function printArrayElements(arr) {
	for (i=0; i<arr.length;i++) {
		console.log(arr[i]);
	}
}
var userIds = [3 , 6, 2, 56];
printArrayElements(inputData);
Outout:
3  
6  
2  
5  
6
```
</p>
</details>

<details>
	<summary>2.Write a program to find largest element in array?</summary>
	<p>

```javascript
function findLargestNumber(arr){
	var max= arr[0];
	for (i=0; i<=arr.length;i++){
		if (arr[i]>max) {
			max=arr[i];
		}
	}
	return max;
}
var data = [3 , 6, 2, 56, 32, 5, 89, 32];
var largetNumber = findLargestNumber(data);
console.log(largetNumber);
Outout: 83
```
		</p>
</details>

<details>
	<summary>3.Write a program to find the smallestNumber in array?</summary>
	<p>
		
```javascript
function findSmallestNumber(numbersArray) {
	var min = inputArray[0];
	for (var i = 1; i < numbersArray.length; i++) {
		if (min > numbersArray[i]){
			min = numbersArray[i];
		}
    	}
}
var inputArray = [3, 6, 2, 56, 32, 5, 89, 32];	
var min = findSmallestNumber(inputArray);
console.log(min);
Output:
2  
```
		</p>
</details>


<details>
	<summary>4.Write a program to find the duplicates in array?</summary>
	<p>
	
```javascript

function findDuplicates(arrayData){
    for (var i = 0; i < arrayData.length; i++) {
        for (var j = i + 1 ; j < arrayData.length; j++) {
             if (arrayData[i]==arrayData[j]) {
                  // got the duplicate element
                   console.log(arrayData[i]);
           			}
       			}
  	 	}
 	}
inputArray = [3 , 6, 2, 56, 32, 5, 89, 32];
findDuplicates(inputArray);

Output:
32  
```

		</p>
</details>
