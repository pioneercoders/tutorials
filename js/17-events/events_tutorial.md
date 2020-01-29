<h3> What is event ?</h3>
<p>a thing that happens or takes place, especially one of importance. </p>

<h3>What is JavaScript Events?</h3>
<p>JavaScript Events are items that transpire based on an action on browser. A document event is the loading of an HTML document. A form event is the clicking on a button.</p>

<p> JavaScript needs a way of detecting user actions so that it knows when to react. When the user does something an event takes place. There are also some events that aren&apos;t directly caused by the user: the load event that fires when a page has been loaded, for instance.</p>

<p>Events are a part of the Document Object Model (DOM) and every HTML element contains a set of events which can trigger JavaScript Code.</p>

<h4>Examples on Events</h4>
<p><b>1.onclick Event:</b>This is the most frequently used event which fires when a user clicks the button in below example. </p>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:250px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	function sayHello() {
	   alert("Hello World")
	}
</script>
</head>
<body>
	<p>Click the following button to see the result</p>
	<button onclick="sayHello()" > Say Hello </button>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview"></iframe>
</div>
</section>

<p><b>2.onfocus/onblur Events:</b>These event's are fires when cursor focus on given element like input,button ect. </p>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:250px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	// Focus = Changes the background color of input to yellow
	function focusFunction() {
		document.getElementById("myInput").style.background = "yellow";
	}
	// No focus = Changes the background color of input to red
	function blurFunction() {
		document.getElementById("myInput").style.background = "red";
	}
</script>
</head>
<body>
	Enter your name: <input type="text" id="myInput" onfocus="focusFunction()" onblur="blurFunction()">
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview1"></iframe>
</div>
</section>


<p><b>3.onselect Event:</b>This event fires when ever select the data of html element in the html page. </p>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview2',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:250px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
	function myFunction() {
		document.getElementById("demo").innerHTML = "You selected data from input field";
	}
</script>
</head>
<body>
	Some text: <input type="text" value="Please Select me!" onselect="myFunction()">
	<p id="demo"></p>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview2"></iframe>
</div>
</section>

