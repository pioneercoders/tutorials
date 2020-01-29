<h4> What is Promise Function? </h4>
<p>The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.</p>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:500px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	console.log("Start");
	// promise defination.
	var isCitiesAvaliable = true;
	var getCitiesPromise = new Promise(function (resolve, reject) {
		if (isCitiesAvaliable) {
			resolve('There are cities in db.');
		} else {
			reject('Error while retriving cities from db.');
		}
	});

	getCitiesPromise.then(function (result) {
		// Resolve callback.
		console.log(result); 
	}, function (result) {
		// Reject callback.
		console.error(result);
	});
	console.log("End");

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
<p>A Promise object is created using the new keyword and its constructor. This constructor takes as its argument a function, called the "executor function". This function should take two functions as parameters. The first of these functions (resolve) is called when the asynchronous task completes successfully and returns the results of the task as a value. The second (reject) is called when the task fails, and returns the reason for failure, which is typically an error object.
</p>
<p>promise can either be fulfilled with a value, or rejected with a reason (error). When either of these options happens, the associated handlers queued up by a promise's then method are called. (If the promise has already been fulfilled or rejected when a corresponding handler is attached, the handler will be called, so there is no race condition between an asynchronous operation completing and its handlers being attached.)</p>

<p>Promise execution is asynchronous, which means that it's executed, but the program won't wait until it's finished to continue with the rest of the code. plase open and see the logs the start, end will print first and after that you may get resolve and reject msg.</p>

