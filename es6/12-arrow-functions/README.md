<h4> What is Arrow Function? </h4>
<p>An arrow function expression has a shorter syntax than a function expression and does not have its own this, arguments, super, or new.target. </p>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:300px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var names = ['Ram', 'Krishna', 'Ravi'];
	names.map((name) => {
	 console.log(name)
	});
	
	var add = (x,y) =>  x + y;
	var sum = add(2,4);
	console.log("sum of 2+4 = " sum);

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
