<h5>What is String?</h5>	
<p>It is an object that represents a sequence of characters.There are two ways to create the String objects in JavaScript.They are</p>	
<ul>
	<li>By string literal</li>
	<li>By string object (using new keyword)</li>
</ul>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:250px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different assignment operators like a ^= b, a |= b, a &= b etc. -->
<script language="javascript" type="text/javascript">
	var str="Pioneercoders";   // string literal
	var str1=new String("hello javascript string"); // string object using new keyword
	console.log("String ", str);
	console.log("String1 ", str1);
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview"></iframe>
    </div>
</section>

<h4>Methods</h4>
<table class="pc-table">
	<tr>
		<td><b>Method Name</b></td>
		<td><b>Description</b></td>
	</tr>
	<tr>
		<td>charAt(index)</td>
		<td>The JavaScript String charAt() method returns the character at the given index.</td>
	</tr>
	<tr>
		<td>concat(str)</td>
		<td>concat(str) method concatenates or joins two strings.</td>
	</tr>
	<tr>
		<td>indexOf(str)</td>
		<td>indexOf(str) method returns the index position of the given string.</td>
	</tr>
	<tr>
		<td>lastIndexOf(str)</td>
		<td>lastIndexOf(str) method returns the last index position of the given string.</td>
	</tr>
	<tr>
		<td>toLowerCase()</td>
		<td>method returns the given string in uppercase letters.</td>
	</tr>
	<tr>
		<td>toUpperCase()</td>
		<td>  method returns the given string in lowerCase letters.</td>
	</tr>
	<tr>
		<td>slice(beginIndex, endIndex)</td>
		<td>this method returns the parts of string from given beginIndex to endIndex. In slice() method, beginIndex is inclusive and endIndex is exclusive.</td>
	</tr>
	<tr>
		<td>trim()</td>
		<td>The JavaScript String trim() method removes leading and trailing whitespaces from the string.</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:500px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different assignment operators like a ^= b, a |= b, a &= b etc. -->
<script language="javascript" type="text/javascript">
	var str="Pioneer Coders";  
	console.log(str.charAt(4));
 
	var tutorial="tutorial";  
	var pcTutorial = str.concat(tutorial);  
	console.log("Concat string ", pcTutorial);
	 
	var index = pcTutorial.indexOf("Coders");  
	console.log("index of coders", index); 
	  
	var lastIndex=pcTutorial.lastIndexOf("Coders");  
	console.log("lastIndex of coders ", lastIndex);
	  
	var pcTutorialLower =pcTutorial.toLowerCase();  
	console.log("pctutorial in lower case ", pcTutorialLower);
	 
	var pcTutorialUpper=pcTutorial.toUpperCase();  
	console.log("pctutorial in upper case ", pcTutorialUpper);
	 
	var sli = pcTutorial.slice(2,5);  
	console.log("after slice ", sli);  
	
	var s1="     javascript trim    ";  
	var s2=s1.trim();  
	console.log("after trim of s1 ",s2); 
	
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview1"></iframe>
    </div>
</section>


<!--
<h4>charAt(index) Method</h4>
<p>The JavaScript String charAt() method returns the character at the given index.</p>
 <h5>Example</h5> 
@CODE_START@@HTML@<script>  
	var str="Pioneercoders";  
	document.write(str.charAt(4));  
</script>@CODE_END@
<div class="min-height-50" id="jsStringCode1"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode1','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>e</p>
</div>

<h4>concat(str) Method</h4>
<p>The JavaScript String concat(str) method concatenates or joins two strings.</p>
 <h5>Example</h5> 
@CODE_START@@HTML@<script>  
	var s1="Pioneercoders";  
	var s2="tutorial";  
	var s3=s1.concat(s2);  
	document.write(s3);  
</script>@CODE_END@
<div class="min-height-50" id="jsStringCode2"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode2','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>Pioneercoders Tutorial</p>
</div>

<h4>indexOf(str) Method</h4>
<p>The JavaScript String indexOf(str) method returns the index position of the given string.</p>
 <h5>Example</h5>
@CODE_START@@HTML@<script>  
	var s1="Pioneercoders javascript Tutorial";  
	var n=s1.indexOf("script");  
	document.write(n);  
</script>@CODE_END@ 
<div class="min-height-50" id="jsStringCode3"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode3','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>18</p>
</div>

<h4>lastIndexOf(str) Method</h4>
<p>The JavaScript String lastIndexOf(str) method returns the last index position of the given string.</p>
 <h5>Example</h5>
@CODE_START@@HTML@<script>  
	var s1="Pioneercoders javascript Tutorial";  
	var n=s1.lastIndexOf("Tutorial");  
	document.write(n);  
</script>@CODE_END@  
<div class="min-height-50" id="jsStringCode4"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode4','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>25</p>
</div>

<h4>toLowerCase() Method</h4>
<p>The JavaScript String toLowerCase() method returns the given string in lowercase letters.</p>
 <h5>Example</h5>
@CODE_START@@HTML@<script>  
	var s1="Pioneercoders javascript Tutorial";  
	var s2=s1.toLowerCase();  
	document.write(s2);  
</script>@CODE_END@  
<div class="min-height-50" id="jsStringCode5"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode5','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>pioneercoders javascript tutorial</p>
</div>

<h4>toUpperCase() Method</h4>
<p>The JavaScript String toUpperCase() method returns the given string in uppercase letters.</p>
 <h5>Example</h5>
@CODE_START@@HTML@<script>  
	var s1="Pioneercoders javascript Tutorial";  
	var s2=s1.toUpperCase();  
	document.write(s2);  
</script>@CODE_END@  
<div class="min-height-50" id="jsStringCode6"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode6','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>PIONEERCODERS JAVASCRIPT TUTORIAL</p>
</div>

<h4>slice(beginIndex, endIndex) Method</h4>
<p>The JavaScript String slice(beginIndex, endIndex) method returns the parts of string from given beginIndex to endIndex. In slice() method, beginIndex is inclusive and endIndex is exclusive.</p>
 <h5>Example</h5>
@CODE_START@@HTML@<script>  
	var s1="abcdefgh";  
	var s2=s1.slice(2,5);  
	document.write(s2);  
</script>@CODE_END@   
<div class="min-height-50" id="jsStringCode7"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode7','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>cde</p>
</div>

<h4>trim() Method</h4>
<p>The JavaScript String trim() method removes leading and trailing whitespaces from the string..</p>
 <h5>Example</h5>
</div>@CODE_START@@HTML@<script>  
	var s1="     javascript trim    ";  
	var s2=s1.trim();  
	document.write(s2);  
</script>@CODE_END@ 
<div class="min-height-50" id="jsStringCode9"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsStringCode9','js')">Try Yourself</button></div>
<div class="output-panel"> 
	<p>javascript trim</p>
</div>
-->
