<h4>What is DataType?</h4>
In maths, When we declare variables, we also specify the type of data and range of the data to that variable.
@CODE_START@@JAVA@Ex: a = x+y; x,y &#8364; Z(integers) and 1<x<10 and 30<y<50 
	numbers for each and every expriment of addition should be with the range.
Expriment 1:  x=4 , y=5 then a = 9
Expriment 2:  x=6 , y=6 then a = 12
@CODE_END@

<p><b><i>JavaScript is a loosely typed or a dynamic language. That means you don't have to declare the type of a variable ahead of time. The type will get determined automatically while the program is being processed.</i></b> It can hold any type of values such as numbers, strings etc.</p>

<p><b>Note :</b>JavaScript does not make a distinction between integer values and floating-point values. All numbers in JavaScript are represented as floating-point values. JavaScript represents numbers using the 64-bit floating-point format defined by the IEEE 754 standard.</p>

<p>There are two types of data types in JavaScript.</p>
<ul>
	<li> 1.Primitive Datatypes</li>
	<li>2.Non-Primitive Datatypes</li>
</ul>

<h4>Primitive Datatypes</h4>
<p>There are five types of primitive data types in JavaScript. They are as follows:</p>
<table class="pc-table">
	<tr>
		<td><b>Datatype</b></td>
		<td><b>Description</b></td>
	</tr>
	<tr>
		<td>String</td>
		<td>represents sequence of characters like "Pioneer Coders". Strings are written with quotes. You can use single or double quotes</td>
	</tr>
	<tr>
		<td>Number</td>
		<td>represents numeric values e.g. 100.20 (with or without decimals)</td>
	</tr>
	<tr>
		<td>Boolean</td>
		<td>represents boolean value either false or true</td>
	</tr>
	<tr>
		<td>Undefined</td>
		<td>represents undefined value</td>
	</tr>
	<tr>
		<td>Null</td>
		<td>represents null i.e. no value at all</td>
	</tr>
</table>


<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:450px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!-- Try to change value and see -->
<script language="javascript" type="text/javascript">
	var carName = "Benz"; // Using Double Quotes
	var carName = 'Benz'; // Using Single Quotes
	console.log("carName::",carName);
	
	var price = 34.00; // Written with decimals
	var age = 34; // Written without decimals
	console.log("price and age ::",price,age);
	
	var isCarGood = true; // true
	var isCarBad = false; // false
	console.log("car is good ::",isCarGood,isCarBad );
	
	var person; // value is undefined, type is undefined
	console.log("person undefined::",person);
	
	var userName = ""; // value is "", type is String
	console.log("userName empty::",userName);
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview"></iframe>
    </div>
</section>


<h4>Non-Primitive Datatypes :</h3>
<p>The non-primitive data types are as follows:</p>
<table class="pc-table">
	<tr>
		<td><b>Datatype</b></td>
		<td><b>Description</b></td>
	</tr>
	<tr>
		<td>Array</td>
		<td>represents group of similar values</td>
	</tr>
	<tr>
		<td>Object</td>
		<td>Object contains properties and functions are written as name:value pairs, separated by commas.</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:250px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!-- Try to change value and see -->
<script language="javascript" type="text/javascript">
	var courses = ["Java", "UI", "DB"]; // array
	var student = {firstName : "Coding", lastName : "Krishna", age : "24"};
	console.log("courses ::",courses);
	console.log("student ::",student);
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview1"></iframe>
    </div>
</section>

<h4>Typeof Operator :</h3>
<p>You can use the JavaScript typeof operator to find the type of a JavaScript variable</p>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview2',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:250px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!-- Try to change value and see -->
<script language="javascript" type="text/javascript">
	var name = "Brendan Eich";
	typeof name; // Returns String
	typeof 3.1415; // Returns Number
	typeof false; // Returns Boolean
	typeof [1, 2, 3, 4]; // Returns Object (not array)
	typeof {name : "Krishna", age : "24"}; // Returns Object
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview2"></iframe>
    </div>
</section>
<p>The typeof operator returns "object" for arrays because in JavaScript arrays are objects.</p>

