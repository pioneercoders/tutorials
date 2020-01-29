<section>
	<iframe width="560" height="315" src="https://www.youtube.com/embed/ZcY_eP2B8VI"
	frameborder="0" allowfullscreen></iframe>
</section>

<h4> What is function ?</h4>
<p> In programming, the concept of functions came from the idea of functions in mathematics. </p>
<p> In mathematics, a function is a relation between a set of inputs and a set of permissible outputs with the property that each input is related to exactly one output. Ex</p>
@CODE_START@@JAVA@f(x) = x*2;
f(1) = 2;
f(2) = 4;
@CODE_END@
@IMG_START@JAVA/function_maths/png@IMG_END@
	
<p><b>Similarly in JS function is a collection of statements that are grouped together to perform a perticular task.</b></p>
<h4>Why we need functions?</h4>
<p>While implementing the business application, a piece of code is repeated for ten times. Same number of lines of code is may repeated for ten times in the other part of the application. This increases redundancy(code duplication), increases the size of the application and application code will become complex. So to avoid these problems functions are used.</p>
	
	<h5>Advantages of functions</h5>
	<ul>
		<li>Code reusability</li>
		<li>size of the application will decrease</li>
		<li>less complexity</li>
	</ul>

<p>function has two parts</p>
<ul>
<li>1) Function Declaration :: defination of the function </li>
<li>2) Function calling :: We have to invoke a function whereever we want to do the same task which we defined in function.</li>
	
	<h4>Function Declaration</h4>
	<p>Function declarations are most familiar and oldest way of defining the functions</p>
	<h5>Syntax:</h5>
	
	@CODE_START@@HTML@function function_name(parameters){
		statement  1
		statement  2 
		etc..
	}@CODE_END@
	<p>A JavaScript function is defined with the <b>function</b> keyword, followed by a name and parentheses<b>()</b>. Function names can contain letters, digits, underscores, and dollar signs(same rules as variables). functions may contains parameters(inputs) its optional<br> </p>
	
	<h4>Function Calling</h4>
	@CODE_START@@HTML@function_name(parameters)@CODE_END@
	
<section >  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:350px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	// Function Declaration
	function display() {
		alert("Welcome to JS world!");
	}
	//Function Calling - remove bellow comments and see.
	//display();
</script>
</head>
<body>
	<button type="button" onclick="display();">Click Me</button>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview"></iframe>
</div>
</section>

	
	<h5>Example: function with parameters</h5>
	<h6>Javascript code to swap the two variables using functions</h6>
	
<section >  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:450px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	// Function Declaration
	function swap(number1, number2) {
		console.log("numbers before swapping: number1 = ", number1, ", ", "number2 = ", number2);
		var temp = number1;
		number1 = number2;
		number2 = temp;
		console.log("numbers after swapping: number1 = ", number1 ,", ", "number2 = ", number2);
	}
	//Function Calling
	//swap(10,20);
	//swap(40,70);
</script>
</head>
<body>
	<button type="button" onclick="swap(30,40);">Clicl me Swap</button>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview1"></iframe>
</div>
</section>


<h5>Example: function returning a value</h5>

<section >  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview2',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:400px;"><xmp><html>
	<head>
	<script language="javascript" type="text/javascript">
	// Function Declaration
	function studentTotalMarks(cMarks, cssMarks, htmlMarks, jsMarks) {
		var sum; //local variable
		sum = cMarks+cssMarks+htmlMarks+jsMarks;
		return sum; // return statement
	}
	//Function Calling
	var sum = studentTotalMarks(75,46,45,38);
	console.log("Student Total Marks: "+ sum);
	</script>
	</head>
	<body>
	
	</body>
</html></xmp>
</div>
<div>
	<iframe id="preview2"></iframe>
</div>
</section>


<!--
<h4>Function Expression</h4>
<p>Expression is nothin but a statement. Function is assigned to some other variables like variable initialization. This type functions can be used only after they are executed</p>
	<h5>syntax</h5>
@CODE_START@@HTML@
	// anonymous function expression
	var myFunction = function () {
		console.log("This statement is from function expression");
	}
	
	(or)
	// syntax for named function expression
	var myFunction = function displayText() {
		console.log("This statement is from function expression");
	}
@CODE_END@
<p>anonymous function expression:- function is declared without function name</p>
<h5>Example</h5>
@CODE_START@@HTML@
<script>
var myFunction = function () {
	alert("Named function Expression");
}
</script>
@CODE_END@
<div class="min-height-50" id="jsFunctionsCode5"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsFunctionsCode5','js')">Try Yourself</button></div>
<h4>Function constructor</h4>
<p>as we know that javascript is a object based programming language. The word constructor is related to object oriented programming.constructor is used to initialize the variables and functions</p>
<h5>Syntax for Function constructor</h5>
@CODE_START@@HTML@ var varibaleName = new Function(parameter1, parameter2,...parametern, "Function body")
@CODE_END@
<p>for the Function() we can pass n number of parameters or arguments</p>
<h5>Example</h5>
@CODE_START@@HTML@<script>
var totalPrice = new Function("price","quantity","return price*quantity;");
var totalBill = totalPrice(100, 50);
document.write(totalBill);// output:5000
</script>@CODE_END@
<div class="min-height-50" id="jsFunctionsCode6"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsFunctionsCode6','js')">Try Yourself</button></div>
-->

<a href="project/download/JS/dynamic_menu" class="cws-button bt-color-3 border-radius alt icon-right">Exercise</a>
