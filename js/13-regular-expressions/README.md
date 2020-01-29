<h4>JavaScript Regular Expression :</h4>
<ul>
	<li>A regular expression is a sequence of characters that forms a search pattern.</li>
	<li>When you search for data in a text, you can use this search pattern to describe what you are searching for.</li>
	<li>A regular expression can be a single character, or a more complicated pattern.</li>
	<li>Regular expressions can be used to perform all types of text search and text replace operations.</li>
</ul>
<h4>Regular Expressions can be constructed in two ways.</h4>
	<ol type="1">
		<li>Regular expression literal.<br>
		</li>
		<li>Calling the constructor function of the RegExp object.</li>
	</ol>
<h4>Regular expression literal</h4>
	<p><b>Syntax</b></p>
	<span>/pattern/modifiers;</span>
	<p>pattern Example</p>
	<p>var pattern=/pc/i
	<br>pc is search pattern and i is the case-insensitive.</p>
<h4>Regular Expression Usage</h4>
<p>Regular expressions can used with the string methods search() and replace().</p>
<ul>
	<li>search() method searches the given pattern in the given string and returns the position of pattern in the given string</li>
	<li>replace() method replaces the provided pattern in the given string and returns the modified string where the pattern is replaced</li>
</ul>
<h4>Example</h4>
@CODE_START@@HTML@<script>
	var string = "Pioneer Coders is a training institute"
	var index = string.search(/coders/i);
	document.write(index);
</script>@CODE_END@
<div class="min-height-50" id="jsRegExCode1"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsRegExCode1','js')">Try Yourself</button></div>
<div class="output-panel">
	<p>8</p>
</div>
<h4>Example </h4>
@CODE_START@@HTML@<script>
	var string = "Welcome Pioneer Coders"
	var index = string.replace(/Welcome/i,"Training Institute");
		document.write(index);
</script>@CODE_END@
<div class="min-height-50" id="jsRegExCode2"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsRegExCode2','js')">Try Yourself</button></div>
<div class="output-panel">
	<p>Training Institute Pioneer Coders</p>
</div>
<h4>Calling the constructor function of the RegExp object</h4>
@CODE_START@@HTML@<script>
	var re = new RegExp('Pioneer');
		document.write(re);
</script>@CODE_END@
<div class="min-height-50" id="jsRegExCode3"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsRegExCode3','js')">Try Yourself</button></div>
<h4>Writing a regular expression pattern</h4>
<p>Brackets: brackets are used to find the range characters.</p>
<h4>A few Special Characters meaning in Regular Expressions</h4>
<table class="pc-table">
	<tr>
		<td>character</td>
		<td>Meaning</td>
	</tr>
	<tr>
		<td>\d</td>
		<td>Matches a digit character in numbers. It is Equivalent to [0-9].</td>
	</tr>
	<tr>
		<td>\D</td>
		<td>Matches any character that is not a digit. Equivalent to [^0-9].</td>
	</tr>
	<tr>
		<td>p$</td>
		<td>	Matches any string with p at the end of it</td>
	</tr>
	<tr>
		<td>^p</td>
		<td>Matches any string with p at the beginning of it</td>
	</tr>
	<tr>
		<td>[a-z]</td>
		<td>Matches the any character between a to z.</td>
	</tr>
	<tr>
		<td>[^a-z]</td>
		<td>Do not Matche the any character between a to z.</td>
	</tr>
	<tr>
		<td>(x|y)</td>
		<td>Matches either x or y.</td>
	</tr>
	<tr>
		<td>x{n}</td>
		<td>Where n is a positive integer. Matches exactly n occurrences of the preceding item x.</td>
	</tr>
	<tr>
		<td>x{n,m}</td>
		<td>Where n and m are positive numbers. Matches at least n and at most m occurrences of the preceding item x.</td>
	</tr>
<table>

<h4>Name Validation Using Regular Expression</h4>
@CODE_START@@HTML@<html>
	<head>
		<style>
			#errormsg {
			color:red;
			font-size:11px;
		}
		</style>
	</head>
	<body>
		<form name ="myform" onsubmit="return validation();" onkeyup="validateName();" onblur="validateName();"> 
			<input type="text" name="name" Placeholder="Name">
			<div id="errormsg"></div>
			<input type="submit">
		</form>
		
		<script>
			function validation(){
				if (document.myform.name.value == "") {
					 document.getElementById('errormsg').innerHTML="*Please enter a username*";
					 return false;
				}
			}
				function validateName() {
				var name = document.myform.name.value;
				var checkName = /[0-9]/; // regular Expression for numbers
				
				if (checkName.test(name)) { //test is javascript function it will return true if name contains digits
					 document.getElementById('errormsg').innerHTML="*Please enter characters only*";
					 return false;
				}
				else{
				 document.getElementById('errormsg').innerHTML="";
					 return true;
				}
			}
		</script>
	</body>
</html>@CODE_END@
<div class="min-height-50" id="jsRegExCode5"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsRegExCode5','js')">Try Yourself</button></div>
<!-- @PROJECT_START@JS/regex@PROJECT_END@
@PROJECT_START@JS/JS_Validations@PROJECT_END@
@PROJECT_START@JS/JS_Validations1@PROJECT_END@
@PROJECT_START@JS/JS_Gmailvalidation@PROJECT_END@ -->
<a href="project/download/JS/regex" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 1</a>
<a href="project/download/JS/JS_Validations" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 2</a>
<a href="project/download/JS/JS_Validations1" class="cws-button bt-color-3 border-radius alt icon-right">Exercise 3</a>	
