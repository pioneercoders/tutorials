
<pc-accordion>

	<accordion-item>
		<accordion-title>1.Write a program to print elements in array?</accordion-title>
		<accordion-content>
		@CODE_START@@JS@var array = [3 , 6, 2, 56];

for (i=0; i<array.length;i++){
    
    console.log(array[i]);
  
}
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

for (i=0; i<=largest;i++){
	if (array[i]>largest) {
		var largest=array[i];
	}
}
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
		@CODE_START@@JS@var array = [3 , 6, 2, 56, 32, 5, 89, 32];
var min = array[0];
for (var i = 1; i < array.length; i++) {
    if (min > array[i])
        min = array[i];
}

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
		@CODE_START@@JS@var oldArray = [3 , 6, 2, 56, 32, 5, 89, 32];
for (var i = 0; i < oldArray.length; i++) {
     for (var j = i + 1 ; j < oldArray.length; j++) {
          if (oldArray[i]==oldArray[j]) {
               // got the duplicate element
                console.log(oldArray[i]);
        }
    }
}@CODE_END@
<div class="output-panel">
	<p>32</p>
</div>
		</accordion-content>
	</accordion-item>
	
<pc-accordion>
