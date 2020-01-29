<iframe width="560" height="315" src="https://www.youtube.com/embed/1nuhemrfnjw" frameborder="0" allowfullscreen></iframe>

<h4>What is Object?</h4>
<p>JavaScript is not a full-blown object-oriented programming language, such as Java, but it is designed on a simple object-based model. An object is a construct with properties that contain JavaScript variables or other objects.</p>

<p> In JavaScript, an object is a standalone entity, with properties and type. Compare it with a cup, for example. A cup is an object, with properties. A cup has a color, a design, weight, a material it is made of, etc. </p>
<ul>
	<li>An Object is a collection of properties.</li>
	<li>Properties are name value pairs attached to the object.</li>
	<li>Property type can be primitive(number, string, float etc.) or reference type</li>
	<li>A property's value can be a function, in which case the property is known as a method.</li>
</ul>

<h4>Object creation in javascript</h4>
<ul type="1">
	<li>Object literal</li>
	<li>Object Keyword</li>
</ul>

<h5>Creating the Object using Object literal</h5>
@CODE_START@@HTML@ var objectName = {
	property1:value1,
	property2:value2,
	property3:method1
		.
		.,
	propertyN:valueN
};@CODE_END@

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:300px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var employeeObject = { id: 1, name: "Coding Krishna", address: "Bangalore",
		work : function(){
			console.log("employee is working ...");
		},
		
		sleep : function(){
			console.log("sleeping...");
		}
	};
	console.log("Employee Id:: ", employeeObject.id)
	employeeObject.work();
</script>
</head>
<body><h3>Please open the console and see the log </h3>
	<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview"></iframe>
</div>
</section>


<h5>Creating the Object using Object keyword</h5>

<h5>Syntax</h5>
@CODE_START@@HTML@<script>var objectName = new Object();
	objectName.property1 = value1;
	objectName.property2 = value2;
</script>@CODE_END@

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:250px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var student = new Object();
	student.name ="Coding Krishna",
	student.id = 1,
	student.location = "bangalore",
	student.coursesJoined = ["Java","HTML","CSS","Javascript"];
	console.log(student.name);
	console.log(student.coursesJoined);
</script>
</head>
<body><h3>Please open the console and see the log </h3>
	<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview1"></iframe>
</div>
</section>

<h3> JavaScript built-in Objects </h3>
JavaScript has several built-in or native objects. These objects are accessible anywhere in your program and will work the same way in any browser running in any operating system. </p>
<p>Here is the list of all important JavaScript Native Objects </p>

<ul>
	<li> Number Object </li>
	<li> String Object </li>
	<li> Array Object </li>
	<li> Date Object </li>
	<li> Math Object </li>
	<li> RegExp Object </li>
</ul>

<h4> Browser Objects </h4>
<ul>
	<li> Window Object </li>
	<li> Navigator Object </li>
	<li> Screen Object </li>
	<li> History Object </li>
	<li> Location Object </li>
</ul>
<h4> HTML DOM Reference </h4>
<ul>
	<li> DOM Document Object </li>
	<li> DOM Element Object </li>
	<li> DOM Attributes Object </li>
	<li> DOM Events </li>
	<li> DOM Style Object </li>
</ul>



<!--
<h4>Object Constructor</h4>
<p>Here are two common patterns for creating objects.</p>
	<h5>1.Constructor Pattern for Creating Objects</h5>
@CODE_START@@HTML@function Topic (01PC, Java, 8, 60){
	this.topicId = "01PC";
	this.topicName = "Java";
	this.totalTopics = 8;
	this.totalClasses = 60;
	this.showName = function () {
		console.log("This is a " + this.topicName);
	}
}@CODE_END@
	<h5>2.Prototype Pattern for Creating Objects</h5>
@CODE_START@@HTML@function Topic () {
	Topic.prototype.topicId = "01PC";
	Topic.prototype.topicName = "Java";
	Topic.prototype.totalTopics = 8;
	Topic.prototype.totalClasses = 60;
	Topic.prototype.showName = function () {
		console.log("This is a " + this.topicName);
	}
}@CODE_END@ -->

<!-- @PROJECT_START@JS/objects@PROJECT_END@
@PROJECT_START@JS/JS_Objects1@PROJECT_END@
@PROJECT_START@JS/JSON_Objects@PROJECT_END@ -->
<a href="project/download/JS/objects" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 1</a>
<a href="project/download/JS/objects1" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 2</a>
<a href="project/download/JS/JSON_Objects" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 3</a>
