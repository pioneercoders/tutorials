
##### 1.Write a program to print elements in array?
```javascript
	inputData = [3 , 6, 2, 56];
	function printArrayElements(numbersArray){
    	for (i=0; i<numbersArray.length;i++){
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

@CODE_START@@JS@var 
		
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
@CODE_END@


<div class="output-panel">
	<p>2</p>
	</div>
		</accordion-content>
	</accordion-item>	
	<accordion-item>
		<accordion-title>4.Write a program to find the duplicates in array?</accordion-title>
		<accordion-content>
		
@CODE_START@@JS@var 

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
	
@CODE_END@

<div class="output-panel">
	<p>32</p>
	</div>
		</accordion-content>
	</accordion-item>
	
<pc-accordion>
