<iframe width="560" height="315" src="https://www.youtube.com/embed/U4z-DKIfe8I" 
frameborder="0" allowfullscreen></iframe><br>
<iframe width="560" height="315" src="https://www.youtube.com/embed/0mlhZ6yAtVo" 
frameborder="0" allowfullscreen></iframe>
<h4> What is Array</h4>
<p>In Maths, An arrangement of objects, pictures, or numbers in columns and rows is called an array. </p>
<p>Similarly in JS, An array is group of memory locations allocated in side by side to store similar type of data.</p>

<ul>
	<li>Each item in an array is called an element</li>
	<li>each element is accessed by its numerical index.</li>
	<li>As shown in the preceding illustration, index numbering begins with 0. ends with array length-1.</li>
	<li>It store the value on the basis of index value.</li>
</ul>

<h4>Why arrays?</h4>
<p>For example if we want to store the ten students total marks. We will declare ten variables and we will store the marks.</p>
@CODE_START@@HTML@<script>
	var firstStudentMarks =300;
	var secondStudentMarks =346;
	var thirdStudentMarks =321;
		.
		.
	var tenthstudentMarks =432;
</script>@CODE_END@

<p> for storing ten students total marks above code fine. Now if we want to store the 100 students total marks above mentioned process is bad way of storing 100 students total marks. We can store using above process but it consumes lot of memory and also increases the processing time.
To over come these problems Array concept is introduced.</p>

<h5>Syntax for declaring Arrays</h5>
@CODE_START@@HTML@var arrayName = [" "," "," ".....];@CODE_END@

<h5>Array Intialization</h5>
@CODE_START@@HTML@var myArray1 = [1,3,5,7,9] // an array with 5 elements
var myArray2 = [5] // an array with 1 element@CODE_END@

<h5>Accessing array elemets</h5>
@CODE_START@@HTML@var firstElement = courses[0]; // JavaScript
var lastElement = courses[courses.length - 1]; // jQuery
@CODE_END@

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:450px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var courses = ["JavaScript", "jQuery", "AngularJs", "React JS","Node"];// array declaration

	function displayCourseList() {
		console.log(courses[0]);
		console.log(courses[1]);
		console.log(courses[2]);
	}
	
	function displayCourseUsingForLoop() {
		for(var i=0;i<courses.length; i++){
			console.log(courses[i]);
		}
	}
	
	//displayCourseList();
	//displayCourseUsingForLoop();
	
</script>
</head>
<body>
	<button type="button" onclick="displayCourseList();">Click Me for Display Course</button>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview"></iframe>
</div>
</section>

	
<h5>Syntax for declaring Arrays using Array keyword</h5>
@CODE_START@@HTML@var arrayName =new Array();@CODE_END@	

<h5>Array Creation</h5>
@CODE_START@@HTML@var courses = ["JavaScript", "jQuery"]; (or)
var courses = new Array("JavaScript", "jQuery");
console.log(courses.length); // 2@CODE_END@

<h5>Loop over an Array</h5>
@CODE_START@@HTML@
<script>
var courses = new Array("JavaScript", "jQuery");
courses.forEach(function (item, index, array) {
document.write(item+"<br>");
});
</script>
@CODE_END@

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:350px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var courses = new Array("JavaScript", "jQuery", "AngularJs", "React JS","Node");// array declaration

	function displayCourseList() {
		courses.forEach(function (item, index, array) {
		console.log("index ", index, "item ", item);
		});
	}	
</script>
</head>
<body>
	<button type="button" onclick="displayCourseList();">Click Me for Display Course</button>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview1"></iframe>
</div>
</section>


<h4>Important methods in array</h4>
<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview2',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:450px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var courses = new Array("JavaScript", "jQuery", "AngularJs", "React JS","Node");// array declaration
	var newLength = courses.push("ES6"); //Add to the end of an Array
	console.log("newLength ",newLength);
	var removeLast = courses.pop(); // remove ES6 (from the end)
	console.log("removeLast ",removeLast);
	var removeFirst = courses.shift();// remove JavaScript (from the front)
	console.log("removeFirst ",removeFirst)
	
	courses.unshift("CSS");// add to the front
	var position = courses.indexOf("JavaScript"); //index of an item in the Array
	console.log("position ",position);
	var removeItemByPos = courses.splice(1 , 1);// this is how to remove an item by index
	
	var shallowCopy = courses.slice( );// this is how to make a copy
	
	function displayCourseList() {
		courses.forEach(function (item, index, array) {
		console.log("index ", index, "item ", item);
		});
	}	
</script>
</head>
<body>
	<button type="button" onclick="displayCourseList();">Click Me for Display Course</button>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview2"></iframe>
</div>
</section>

<h5>Array Properties</h5>
<table class="pc-table">
<tr> 
	<td><b>Property </b></td>
	<td><b>Description</b></td>
</tr>
</tr>
<tr> 
	<td>constructor</td>
	<td>Returns a reference to the array function that created the object.</td>
</tr>
<tr> 
	<td>index</td>
	<td>The property represents the zero-based index of the match in the string</td>
</tr>		
<tr> 
	<td><span></span>input</td>
	<td>This property is only present in arrays created by regular expression matches.</td>		
</tr>						
<tr> 
	<td>prototype </td>
	<td>The prototype property allows you to add properties and methods to an object.</td>		
</tr>		
<tr> 
	<td><span></span>length</td>
	<td>Reflects the number of elements in an array.</td>
</tr>
</table>	
<p><b>Array Methods</b></p>
<table class="pc-table">
<tr> 
	<td><b>Method </b></td>
	<td><b>Description</b></td>
</tr>
<tr> 
	<td>concat()</td>
	<td>Returns a new array comprised of this array joined with other array(s) and/or value(s).</td>
</tr>
<tr> 
	<td>every() </td>
	<td>Returns true if every element in this array satisfies the provided testing function.</td>
</tr>
<tr> 
	<td>filter()</td>
	<td>Creates a new array with all of the elements of this array for which the provided filtering function returns true.</td>
</tr>
<tr> 
	<td>forEach()</td>
	<td>Calls a function for each element in the array.</td>
</tr>
<tr> 
	<td>indexof()</td>
	<td>Returns the first (least) index of an element within the array equal to the specified value, or -1 if none is found.</td>
</tr>
<tr> 
	<td>join()</td>
	<td>Joins all elements of an array into a string.</td>
</tr>		
<tr> 
	<td>lastIndexOf() </td>
	<td>Returns the last (greatest) index of an element within the array equal to the specified value, or -1 if none is found.</td>
</tr>
<tr> 
	<td>map()</td>
	<td>Creates a new array with the results of calling a provided function on every element in this array.</td>
</tr>
<tr> 
	<td>pop()</td>
	<td>Removes the last element from an array and returns that element.</td>
</tr>
<tr> 
	<td>push()</td>
	<td>Adds one or more elements to the end of an array and returns the new length of the array.</td>
</tr>
<tr> 
	<td>reduce()</td>
	<td>Apply a function simultaneously against two values of the array (from left-to-right) as to reduce it to a single value.</td>
</tr>
<tr> 
	<td>reduceRight() </td>
	<td>Apply a function simultaneously against two values of the array (from right-to-left) as to reduce it to a single value.</td>
</tr>
<tr> 
	<td>reverse()</td>
	<td>Reverses the order of the elements of an array -- the first becomes the last, and the last becomes the first.</td>
</tr>
<tr> 
	<td>shift()</td>
	<td>Removes the first element from an array and returns that element.</td>
</tr>
<tr> 
	<td>slice()</td>
	<td>Extracts a section of an array and returns a new array.</td>
</tr>
<tr> 
	<td>some()</td>
	<td>Returns true if at least one element in this array satisfies the provided testing function.</td>
</tr>	
<tr> 
	<td>toSource() </td>
	<td>Represents the source code of an object</td>
</tr>
<tr> 
	<td>sort()</td>
	<td>Represents the source code of an object</td>	
</tr>	
<tr> 
	<td>splice()</td>
	<td>Removes the last element from an array and returns that element.</td>
</tr>	
<tr> 
	<td>unshift()</td>
	<td>Adds one or more elements to the front of an array and returns the new length of the array.</td>
</tr>
<tr> 
	<td><span></span>toString()</td>
	<td>Returns a string representing the array and its elements.</td>
</tr>
</table>
