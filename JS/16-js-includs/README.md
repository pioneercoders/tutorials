		<h4>How can we include the Javascript into the web page ?</h4>
		<p>There are three ways to include the javascript code into the webpage</p>
			<ul>
				<li>Inline<li>
				<li>Inside the head tag<li>
				<li>External file<li>
			</ul>
		<h4>Inline Style</h4>
		<p>javascript code can be included into the web page using &lt;script&gt; tag</p>
@CODE_START@@HTML@<html>
	<head></head>
	<body>
		<script>
			JavaScript Code
		</script>
	</body>
</html>@CODE_END@	
<h4>Inside the &lt;head&gt;</h4>	
@CODE_START@@HTML@<html>
	<head>
		<script>
			JavaScript Code
		</script>
	</head>
	<body>
	</body>
</html>@CODE_END@
<h4>External JS file</h4>
<p>code can be written  and save the file with the .js extension</p>
@CODE_START@@HTML@<html>
	<head>
		<script language="javascript" type="text/javascript" src="myjavascript.js"></script>
	</head>
	<body>
	</body>
</html>@CODE_END@
<p>the external javascript file can be included in the head tag or at the end of the body tag. It is recomended to include the js file at the end of body tag.</p>
		
	<p>The script tag takes two important attributes -</p>
	
	<p><b>Language </b>This attribute specifies what scripting language you are using. Typically, its value will be javascript.</p>
		
	<p><b>Type </b>This attribute is what is now recommended to indicate the scripting language in use and its value should be set to "text/javascript".</p>
