##### 1.Write a program to print elements in array?

```javascript
inputData = [3 , 6, 2, 56];
function printArrayElements(numbersArray) {
	for (i=0; i<numbersArray.length;i++) {
		console.log(numbersArray[i]);
	}
}
printArrayElements(inputData);'
Outout:
3  
6  
2  
5  
6
```
#### 2.Write a program to find largest element in array?
		
```javascript
array = [3 , 6, 2, 56, 32, 5, 89, 32];
var largest= 0;

function findLargestNumber(numbersArray){
	for (i=0; i<=largest;i++){
		if (numbersArray[i]>largest) {
			largest=numbersArray[i];
		}
	}
}

findLargestNumber(array);
console.log(largest);
Outout: 83
```
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
