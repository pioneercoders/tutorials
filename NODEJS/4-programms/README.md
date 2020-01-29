
<pc-accordion>

	<accordion-item>
		<accordion-title>1.Write a program to print elements in array?</accordion-title>
		<accordion-content>
		@CODE_START@@JS@var inputData = [3 , 6, 2, 56];

function printArrayElements(numbersArray){
    for (i=0; i<numbersArray.length;i++){
        console.log(numbersArray[i]);
    }
}

printArrayElements(inputData);
@CODE_END@
<div class="output-panel">
	<p>3<br>6<br>2<br>56</p>
</div>
		</accordion-content>
	</accordion-item>
	<accordion-item>
		<accordion-title>2.Write a program to find largest element in array?</accordion-title>
		<accordion-content>
		@CODE_START@@JS@var array = [3 , 6, 2, 56, 32, 5, 89, 32];
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
@CODE_END@
<div class="output-panel">
	<p>89</p>
</div>
		</accordion-content>
	</accordion-item>
	
	<accordion-item>
		<accordion-title>3.Write a program to find the smallestNumber in array?</accordion-title>
		<accordion-content>
		@CODE_START@@JS@var inputArray = [3, 6, 2, 56, 32, 5, 89, 32];
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
		@CODE_START@@JS@var inputArray = [3 , 6, 2, 56, 32, 5, 89, 32];
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
