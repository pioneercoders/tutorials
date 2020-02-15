<h4>How to include JS in HTML document? </h4>
<p>There are three ways to include the javascript code into the webpage</p>

<ul>
	<li>Inline</li>
	<li>Embedded</li>
	<li>External file</li>
</ul>

<h4>Inline JS</h4>
<p>javascript code can be included inside html tag</p>

```html
<!DOCTYPE html>
<html>
<head></head>
<body>
	<a href="#" onclick="(function(){alert(this);})()">Click Me</a>
</body>
</html>
```

<h4>Embedded JS</h4>
Write the js code inside `<script>` tag and with in `<head>` tag.

```html
<!DOCTYPE html>
<html>
<head>
	<script>
		function hello(){
			console.log('Welcome to pioneer coders.');
		}
	</script>
</head>
<body>
	<a href="#" onclick="hello()">Click Me</a>
</body>
</html>
```

<h4>External JS file</h4>
<p>Write JS code in seperate file and save with .js extension and include with script tag.</p>

```html
<!DOCTYPE html>
<html>
<head>
	<script language="javascript" type="text/javascript" src="main.js"></script>
</head>
<body>
	<a href="#" onclick="hello()">Click Me</a>
</body>
</html>
```

<p>the external javascript file can be included in the head tag or at the end of the body tag. It is recomended to include the js file at the end of body tag.</p>
