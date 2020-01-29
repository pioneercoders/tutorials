<h3>What is OOPs?</h3>
	
<p>The foundations of any kind of program constructed in JavaScript might be imagined in terms of Objects. A good example of this idea should be to have a look at a handful of sample business requirements for a product.</p>
<p>Imagine that we are tasked with constructing a software program intended to keep track of an actual public library system. This system must keep track of each of the branches associated with the libraries, the whole set of materials that can be contained in the branches, and additionally all of the people that may need to access books from the library&rsquo;s branch.</p>
	
<p>The first thing we&rsquo;re able to do is examine those specs and pinpoint all of the keywords which happen to be nouns. For the record, a noun is actually a person, place or thing. Which means, if we analyze our requirements we discern these particular nouns:</p>
<ul>
	<li>Library</li>	
	<li>Book</li>
	<li>Branch</li>
	<li>Customer</li>
</ul>

<p> All these words represent Objects in JavaScript. This really is, in essence, Object Oriented programming. What we can now go about doing, is in fact arrange these four Objects on to some sort of piece of paper, and begin to distinguish what sort of attributes each one of these Objects contains. What do I mean by the attributes? Well, in O-O development this is known as identifying the "has a" relationships. To provide an example, a Branch "has an" address, a Book "has a" title, a Customer "has a" name. We will map out the most important attributes that each one of these Objects contain, and build ourselves a terrific starting point for the design of our JavaScript application.</p>
		 
<p>Object Oriented development allows developers to think in terms of real life &rdquo;things&rdquo; or Objects, and simply solve issues with all those Objects.</p>				 

<p>As a language that has the Object Oriented feature, JavaScript supports the following fundamental concepts:</p>
<ul>
	<li>Polymorphism</li>
	<li>Inheritance</li>
	<li>Encapsulation</li>
	<li>Abstraction</li>
	<li>Classes</li>
	<li>Objects</li>
	<li>Instance</li>
	<li>Method</li>
	<li>Message Parsing</li>
</ul>


<h5>Creating the Object using Object literal</h5>

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
<p>employeeObject is a perfectly nice for one employee why because id, name and address are hardcoded, it would be helpful if we could define a pattern for any employee.</p>

<h5>Creating the Object using new keyword</h5>
<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:350px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var employee = function(id,name, address){
		this.id = id; 
		this.name = name; 
		this.address = address;
		work = function(){
			console.log("employee ", this.name," is working ...");
		};
		sleep = function(){
			console.log("employee ", this.name,"sleeping...");
		}
	};
	var emp1 = new employee(1,"Krishna", "Bangalore");
	var emp2 = new employee(2,"Hari", "hyd");
	console.log("Employee 1:: ", emp1.id,emp1.name);
	console.log("Employee 2:: ", emp2.id, emp2.name);
	
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
<p> In above approch we can create n number of employee objects and we can provide the employee data. the new keyword is used to create object of the employee.</p>

