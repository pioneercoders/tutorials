<p> In the JavaScript there are two types of scopes:</p>
<ul> 
	<li> Global Scope </li>
	<li> Local Scope </li>
</ul>
<p>A variable that is declared outside a function definition is a global variable, and its value is accessible and modifiable throughout your program. A variable that is declared inside a function definition is local. It is created and destroyed every time the function is executed, and it cannot be accessed by any code outside the function. </p>

<section >  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:350px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var pi = 3.45;
	
	function area(r) {
		var a =  pi * r * r;
		return a;
	}
	var ar = area(3);
	console.log("area of circle ", ar);
</script>
</head>
<body>
	
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview"></iframe>
</div>
</section>
<p> in above example pi and ar are gobal variables and area function is global function. variable a inside fuction is local variable, it will create everytime function executed and destoried after completion execution of function.</p>

	
