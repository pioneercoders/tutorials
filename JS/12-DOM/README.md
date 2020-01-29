<iframe width="560" height="315" src="https://www.youtube.com/embed/TGEaMf0etTg" frameborder="0" allowfullscreen></iframe><br>
<h4>What is the DOM?</h4>
<ul>
	<li>Abbrievated DOM as <b>Document Object Model</b>.</li>
	<li>A web page or Website which is loaded into the browser window is considered as document object. </li>
	<li>using document or window object, we can access each and every element in a web page.</li>
	<li>DOM is <b>programming interface</b> for HTML</li>
	<li>DOM provides <b>structured representation</b> of the document(observe the bellow diagram) as object that have properties and methods.</li>
</ul>
<h4>HTML DOM structure</h4>
@IMG_START@JS/html_dom/jpg@IMG_END@

<ul>
	<li>Javascript has ability to access and modify all the HTML elements present in the HTML page using document object.</li>
	<li>Javascript has ability to change the all the elements styles using document object.</li>
	<li>Javascript has ability to add and remove content to HTML page using innerHTML</li>	
</ul>

<h4>DOM methods</h4>
<p>Using DOM methods we can perform actions on the HTML elements. For example if we want to change the HTML paragraph(&lt;p&gt; &lt;/p&gt;) element content we will use DOM methods.
The following are the DOM methods to access the HTML elements.</p>
<table class='grid-md-12 pc-table'>
	<tr>
		<td>DOM method</td>
		<td>Description</td>
	</tr>
	<tr>
		<td>document.getElementById(id)</td>
		<td>Finding HTML Elements by element id</td>
	</tr>
	<tr>
		<td>getElementsByClassName(class)</td>
		<td>Finding HTML Elements by element className</td>
	</tr>
	<tr>
		<td>getElementsByName</td>
		<td>Finding HTML Elements by element name</td>
	</tr>
	<tr>
		<td>getElementsByTagName</td>
		<td>Finding HTML Elements by element tag name</td>
	</tr>
</table>
<h4>Changing HTML elements</h4>
<table class='grid-md-12 pc-table'>
	<tr>
		<td>DOM </td>
		<td>Description</td>
	</tr>
	<tr>
		<td>element.innerHTML =  new html content</td>
		<td>Change the inner HTML(content) of an element</td>
	</tr>
	<tr>
		<td>element.attribute = new value</td>
		<td>Change the attribute(ex:border) value of an HTML element(ex:table)</td>
	</tr>
	<tr>
		<td>element.setAttribute(attribute, value)</td>
		<td>Change the attribute value of an HTML element</td>
	</tr>
	<tr>
		<td>element.style.property = new style</td>
		<td>Change the style of an HTML element</td>
	</tr>
</table>


<h4>Changing HTML element content by its id</h4>
<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:250px;"><xmp><html>
	<body>
		<p id="pc">Hello Pioneer Coders.</p>
		<button type="button" onclick="changeContent();">Click here to change the text</button>
	</body>
	<script>
		function changeContent(){
			var pcElement = document.getElementById("pc");
			pcElement.innerHTML = "Welcome to Pioneer Coders." //
		}
	</script>
</html>
</xmp>
	</div>
	<div>
        <iframe id="preview"></iframe>
    </div>
</section>

<h4>Changing HTML element content by its className</h4>
<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:250px;"><xmp><html>
		<body>
		<div class="pc">Pioneer Coders provides training.</p>
		<div class="pc">Pioneer Coders provides placements</p>
		<p id="one"></p>
		<button type="button" onclick="changeContent();">Click here to change the text</button>
	</body>
	<script>
		function changeContent(){
			var pcElements = document.getElementsByClassName("pc");
			document.getElementById("one").innerHTML = (pcElements[0].innerHTML)+" "+(pcElements[1].innerHTML);
		}
	</script>
</html></xmp>
	</div>
	<div>
        <iframe id="preview1"></iframe>
    </div>
</section>


<h4>Changing HTML element content by its TagName</h4>
<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview2',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:250px;"><xmp><html>
	<body>
		<p class="hello">Pioneer Coders</p>
		<p id="second"></p>
		<button type="button" onclick="changeContent();">Click here to change the text</button>
	</body>
	<script>
		function changeContent(){
			var p= document.getElementsByTagName("p");
			document.getElementById("second").innerHTML = (p[0].innerHTML)+"text is from above paragraph";
		}
	</script>
</html></xmp>
	</div>
	<div>
        <iframe id="preview2"></iframe>
    </div>
</section>

<a href="project/download/JS/dom" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 1</a>
<a href="project/download/JS/JS_DOM" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 2</a>
<a href="project/download/JS/popupclose" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 3</a>
