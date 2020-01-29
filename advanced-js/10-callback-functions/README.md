<h4> What is Callback Functions? </h4>
<p>In Javascript we can pass a function to another function as parameter, calling that parameter function, we called as callback function. </p>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:500px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	var success = function(){
		console.log("getcities success show results to user ...");
	}
	var failure = function(){
		console.log("getcities failed show error msg to user...");
	}
	
	var getCities = function(successCallback,failureCallback) {
		//getcities from db. 
		var isCitiesAvaliable = true;
		if(isCitiesAvaliable){
			successCallback();
		}else{
			failureCallback();
		}
	}
	
	getCities(success,failure);

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
<p>In above example, success and failure are the functions which passed as parameter to getCities function. On succesfull retrival of the cities wer are calling successCallback and if any failure we are calling failureCallback functions. </p>
