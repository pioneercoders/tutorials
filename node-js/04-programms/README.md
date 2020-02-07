
<details>
  <summary>1.Write a program to print elements in array?</summary>
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
</details>

<details>
  <summary>2.Write a program to find largest element in array?</summary>	
```javascript
function findLargestNumber(arr){
	var largest= 0;
	for (i=0; i<=arr.length;i++){
		if (arr[i]>largest) {
			largest=arr[i];
		}
	}
	return largest;
}
var data = [3 , 6, 2, 56, 32, 5, 89, 32];
var largetNumber = findLargestNumber(data);
console.log(largetNumber);
Outout: 83
```
</details>

#### 3.Write a program to find the smallestNumber in array?

```javascript
inputArray = [3, 6, 2, 56, 32, 5, 89, 32];
var min = inputArray[0];
function findSmallestNumberInArray(numbersArray){
for (var i = 1; i < numbersArray.length; i++) {
       if (min > numbersArray[i]){
           min = numbersArray[i];
        	}
    	     }
	}
findSmallestNumberInArray(inputArray);
console.log(min);
Output:
2  
```

#### 4.Write a program to find the duplicates in array?
	
```javascript
inputArray = [3 , 6, 2, 56, 32, 5, 89, 32];
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

findDuplicates(inputArray);

Output:
32  
```
