<h4> What is a Class?</h4>
<p> Classes are in fact "special functions", and just as you can define function expressions and function declarations, the class syntax has two components: class expressions and class declarations.</p>

<h4> Class declarations</h4>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:450px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	class Employee{
		constructor(id,name, address){
			this.id = id; 
			this.name = name; 
			this.address = address;
		}
		work(){
			console.log("employee ", this.name," is working ...");
		}
		sleep(){
			console.log("employee ", this.name,"sleeping...");
		}
	};
	var emp1 = new Employee(1,"Krishna", "Bangalore");
	var emp2 = new Employee(2,"Hari", "hyd");
	console.log("Employee 1:: ", emp1.id, emp1.name);
	console.log("Employee 2:: ", emp2.id, emp2.name);
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

<h4>Constructor</h4>
<p> The constructor method is a special method for creating and initializing an object created with a class. There can only be one special method with the name "constructor" in a class. A SyntaxError will be thrown if the class contains more than one occurrence of a constructor method.</p>

<h4> Prototype methods</h4>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:550px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	class Rectangle {
	  constructor(height, width) {
		this.height = height;
		this.width = width;
	  }
  
	  getArea() {
		return this.calcArea();
	  }

	  calcArea() {
		return this.height * this.width;
	  }
	}

const square = new Rectangle(10, 10);
var area = square.getArea();
console.log(area);
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






