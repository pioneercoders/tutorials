
	<iframe width="560" height="315" src="https://www.youtube.com/embed/ll3mjjrS2lI" frameborder="0" allowfullscreen></iframe><br>

<h4>DOM CSS</h4>
<p>adding styles to HTML page  Syntax: element.style = new style </p>

```html
	<body>
		<div id="pc">Pioneer Coders is best place to learn </div>
		<button type="button" onclick="changeStyle();">Click here to change the color</button>
	</body>
	<script>
		function changeStyle(){
			var pcElement = document.getElementById("pc");
			pcElement.style.color = "green";
			pcElement.style.border = "2px solid black";
			pcElement.style.margin = "5px";
		}
	</script>
</html>
```
<div>
        <iframe id="preview3"></iframe>
</div>


<a href="project/download/JS/dom" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 1</a>
<a href="project/download/JS/JS_DOM" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 2</a>
<a href="project/download/JS/popupclose" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 3</a>	
