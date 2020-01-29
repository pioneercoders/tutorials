<h4> What is a prototype?</h4>
<p> A prototype is a model that displays the appearance and behavior of an application or product early in the development lifecycle.</p>
<p> In case of Javascript, A prototype is a model that displays the appearance and behavior of object early in the object lifecycle.</p>
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
		this.work = function(){
			console.log("employee ", this.name," is working ...");
		};
		this.sleep = function(){
			console.log("employee ", this.name,"sleeping...");
		}
	};
	var emp1 = new employee(1,"Krishna", "Bangalore");
	var emp2 = new employee(2,"Hari", "hyd");
	console.log("Employee 1:: ", emp1.id,emp1.name);
	console.log("Employee 2:: ", emp2.id, emp2.name);
	emp1.work();
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
<h5> Now if i want to add mobile number to all my employees? </h5>
<p> We can do this by using the prototype keyword, even after having defined the prototype object.</p>
<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview2',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:450px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var employee = function(id,name, address){
		this.id = id; 
		this.name = name; 
		this.address = address;
		this.work = function(){
			console.log("employee ", this.name," is working ...");
		};
		this.sleep = function(){
			console.log("employee ", this.name,"sleeping...");
		}
	};
	var emp1 = new employee(1,"Krishna", "Bangalore");
	var emp2 = new employee(2,"Hari", "hyd");
	console.log("Employee 1:: ", emp1.id,emp1.name);
	console.log("Employee 2:: ", emp2.id, emp2.name);
	employee.prototype.mobile;
	emp1.mobile="123456789";
	emp2.mobile="987654321"
	console.log("Employee 1:: ", emp1.id,emp1.name,emp1.mobile);
	console.log("Employee 2:: ", emp2.id, emp2.name,emp2.mobile);
</script>
</head>
<body><h3>Please open the console and see the log </h3>
	<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview2"></iframe>
</div>
</section>




