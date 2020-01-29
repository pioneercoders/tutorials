
<p>JavaScript operators are symbols that are used to perform operations on operands.</p>
<p>Javasript operators are categorized into following types.</p>
<ul>
	<li>Assignment Operators</li>
	<li>Arithmetic Operators</li>
	<li>Relational(Comparison) Operators</li>
	<li>Logical Operators</li>
	<li>Bitwise Operators</li>
	<li>Conditional(ternary) operators</li>
	<li>Comma operator</li>
	<li>Unary operators</li>
</ul>

<h4>Assignment Operators</h4>
<p>Definition: Assignment operators assigns value to a variable using simple equl(=) operator.</p>
<p>The assignment operators asigns right operand value to its left operand. The right operand value can anything it can be simple integer or string or an expression.</p>

<h4>Shorthand Assignment operators</h4>
<table class="pc-table">
	<tr>
		<td>Name</td>
		<td>ShortHand Operator</td>
		<td>Meaning</td>
	</tr>
	<tr>
		<td>Assignment</td>
		<td>a = b</td>
		<td>a = b</td>
	</tr>
	<tr>
		<td>Addition assignment</td>
		<td> a += b</td>
		<td>a = a+b</td>
	</tr>
	<tr>
		<td>Subtraction assignment</td>
		<td>a -+ b</td>
		<td>a = a-b</td>
	</tr>
	<tr>
		<td>Multiplication assignment</td>
		<td>a *= b</td>
		<td>a = a*b</td>
	</tr>
	<tr>
		<td>Division assignment</td>
		<td>a /b=b</td>
		<td>a = a/b</td>
	</tr>
	<tr>
		<td>Remainder assignment</td>
		<td>a %= b</td>
		<td>a = a%b</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:400px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different assignment operators like a ^= b, a |= b, a &= b etc. -->
<script language="javascript" type="text/javascript">
	var a = 100, b = 200; 
	var result = a += b; 
	console.log("(a += b) ="+result);
	var result = a-=b; 
	console.log("(a-=b) ="+result);
	var result = a*=b; 
	console.log("(a*=b) ="+result);
	var result = a/=b; 
	console.log("(a/=b) ="+result);
	var result = a%=b; 
	console.log("(a%=b) ="+result);
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview"></iframe>
    </div>
</section>

<h4>Arithmetic Operators</h4>
<p>Arithmetic operators take numaric operands and returns single numaric operand.</p>
<table class="pc-table">
	<tr>
		<td><b>Operator</b></td>
		<td><b>Description</b></td>
		<td><b>Example</b></td>
	</tr>
	<tr>
		<td>+</td>
		<td>Addition</td>
		<td>10+20 = 30</td>
	</tr>
	<tr>
		<td>-</td>
		<td>Subtraction</td>
		<td>20-10 = 10</td>
	</tr>
	<tr>
		<td>*</td>
		<td>Multiplication</td>
		<td>10*20 = 200</td>
	</tr>
	<tr>
		<td>/</td>
		<td>Division</td>
		<td>20/10 = 2</td>
	</tr>
	<tr>
		<td>%</td>
		<td>Modulus(Remainder)</td>
		<td>20%10 = 0</td>
	</tr>
	<tr>
		<td>++</td>
		<td>Increment</td>
		<td>var a = 10; a++; now a=11;</td>
	</tr>
	<tr>
		<td>--</td>
		<td>Deccrement</td>
		<td>var a = 10; a--; now a=9;</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:400px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different values... . -->
<script language="javascript" type="text/javascript">
	var a = 40, b = 20, c = "PC"; 
	console.log("a + b =", a + b);
	console.log("a - b =", a - b);
	console.log("a/b =", a/b);
	console.log("a%b =", a%b);
	console.log("a + b + c =", a + b + c);
	console.log("a++ =", a++);
	console.log("b-- =", b--);
	console.log("Pioneer"+"Coders"); 
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview1"></iframe>
    </div>
</section>
<p>The string operator(+) cancatenates(adds) two strings, returning another string.</p>


<h4>Relational(Comparison) Operators </h4>
<p>A comparison operator compares both left and right operands and returns a logical(true or false) value. The oprands can be numarical values or strings or objects.</p>
 <ul>
	<li>if the comparision is true then it will return true</li>
	<li>if the comparision is false then it will return false</li>
 </ul>
 <h4>What happens if the operands are of different types?</h4>
 <p>For example mistakenly the left operand is numaric value and right operand is string type. if we are trying to compare the two operands which are of two different data types. JavaScript attempts to convert them to an appropriate type for the comparison. This behavior generally results in comparing the operands numerically.</p>
<table class="pc-table">
	<tr>
		<td>Operator</td>
		<td>Description</td>
		<td>return value</td>
	</tr>
	<tr>
		<td>Equal (==)</td>
		<td>Returns true if the operands are equal.</td>
		<td>(14 == 14)  (4 == '14') ("14" == 14)</td>
	</tr>
	<tr>
		<td>Not equal (!=)</td>
		<td>Returns true if the operands are not equal.</td>
		<td> (14 != 15), (14 != '15'), ("14" !=15)</td>
	</tr>
	<tr>
		<td>Strict equal (===)</td>
		<td>Returns true if the operands... </td>
		<td>5 == 5</td>
	</tr>
	<tr>
		<td>greater than (>)</td>
		<td>Returns true if the value is greater</td>
		<td>(5>1), (10>3)</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview2',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:400px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different values... . -->
<script language="javascript" type="text/javascript">
	var a = 14, b = 15; 
	console.log("(a == b) ="+(a==b));
	console.log("(a < b) ="+(a<b));
	console.log("(a>b) ="+(a>b));
	console.log("(a!=b) ="+(a!=b));
	console.log("(a<=b) ="+(a<=b));
	console.log("(a<=b) ="+(a<=b));
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview2"></iframe>
    </div>
</section>


<h4>Logical Operators :</h4>
<p>Logincal operators are three types</p>
	<ul>
		<li>Logical AND(&&)</li>
		<li>Logical OR (||)</li>
		<li>Logical NOT(!)</li>
	</ul>
<table class="pc-table">
	<tr>
		<td><b>Operator</b></td>
		<td><b>Description</b></td>
		<td><b>Example</b></td>
	</tr>
	<tr>
		<td>Logical AND (&&)</td>
		<td>returns true if both the operands are true</td>
		<td>(14==15 && 23==53) = false</td>
	</tr>
	<tr>
		<td>Logical OR (||)</td>
		<td>returns true if any of the two operands is true</td>
		<td>(14==15 || 23==53) = false</td>
	</tr>
	<tr>
		<td>Logical NOT (!)</td>
		<td>returns true if the expression is false(it inverts the Actual result)</td>
		<td>!(14==15) = true</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview3',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:400px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different values... -->
<script language="javascript" type="text/javascript">
	var a = 14, b = 15, c=23, d=53; 
	var andresult = (a == b) && (c == d); 
	console.log("(a == b) && (c == d) =", andresult);
	var orresult = (a >= b) || (c <=	 d);
	console.log("(a >= b) || (c =< d) =", orresult);
	var result = !andresult; 
	console.log("!andresult ="+result);
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview3"></iframe>
    </div>
</section>


<h4>Bitwise Operators :</h4>
<p>The name itself indicates that it performs operations using bits(1 byte = 8 bits). Even if we enter decimal values like 10 or 20, 
the system automatically converts decimal values into binary representation. To understand go through following example</p>
<table class="pc-table">
	<tr>
		<td><b>Expression</b></td>
		<td><b>Result</b></td>
		<td><b>Binary Description</b></td>
	</tr>
	<tr>
		<td>4&5</td>
		<td>4</td>
		<td>100&101 = 100</td>
	</tr>
	<tr>
		<td>4|5</td>
		<td>5</td>
		<td>100 | 101 = 101</td>
	</tr>
	<tr>
		<td>4^5</td>
		<td>2</td>
		<td>100 ^ 101 = 010</td>
	</tr>
	<tr>
		<td>~5</td>
		<td>2</td>
		<td>~101 = 010</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview4',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:400px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different values... -->
<script language="javascript" type="text/javascript">
	var a = 2, b = 3;  
	console.log("(a & b) =", (a & b) );
	console.log("(a | b) =", (a | b) );
	console.log("(~b) =", (~b) );
	console.log("(a<<b) =", (a<<b) ); 
	console.log("(a>>b) =", (a>>b) );
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview4"></iframe>
    </div>
</section>


<h4>Ternary Operators(conditional Operators)</h4>
<p>Ternary operator requires three operators</p>
@CODE_START@@HTML@condition? result1: result2@CODE_END@
<p>If the condition is true it returns the results1, Otherwise it returns result2.</p>
<h4>Finding the given number is even or odd using Ternary Operators</h4>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview5',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:400px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different values... -->
<script language="javascript" type="text/javascript">
	var number = 10;
	(number%2==0)?console.log("number is even"):console.log("number is odd");
	
	var number1 = 10, number2 = 20;
	(number1>number2)?console.log(number1+" is big"):(number1<number2)?console.log(number2+" is big"):console.log("number1 and number2 are equal");
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview5"></iframe>
    </div>
</section>


<h4>Other Operator</h4>
<table class="pc-table">
	<tr>
		<td><b>Operator</b></span>
		<td><b>Operator type</b></td>
		<td><b>Description</b></span>
	</tr>
	<tr>
		<td>(?:)</td>
		<td>Conditional Operator </td>
		<td>Conditional Operator returns value based on the condition. It is like if-else.</td>
	</tr>
	<tr>
		<td>,(comma)</td>
		<td>Comma Operator</td>
		<td>Comma Operator allows multiple expressions to be evaluated as single statement.</td>
	</tr>
	<tr>
		<td>delete</td>
		<td>Unary Operator</td>
		<td>Delete Operator deletes a property from the object or an array.</td>
	</tr>
		<tr>
		<td>typeof</td>
		<td>Unary Operator</td>
		<td>checks the type of object.</td>
	</tr>
	<tr>
		<td>void</td>
		<td>Unary Operator</td>
		<td>it discards the expression's return value.</td>
	</tr>
	<tr>
		<td>in</td>
		<td>Relational Operator</td>
		<td>In Operator checks if object has the given property</td>
	</tr>
	<tr>
		<td>Instanceof</td>
		<td>Relational Operator</td>
		<td>checks if the object is an instance of given type</td>
	</tr>
	<tr>
		<td>new</td>
		<td>new operator </td>
		<td>creates an instance (object)</td>
	</tr>
</table>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview6',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:400px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different values... -->
<script language="javascript" type="text/javascript">
	var myArray = [1,2,3,4,5];
	delete myArray[2]; //deletes element at index 2 in myArray.
	console.log(myArray);
	var InstituteName = "PioneerCoders";
	console.log(typeof(InstituteName)); // prints string
	var date = new Date() // create date object with today's date and time. 
	delete date; // deletes the date object;
	
	for(var i=0,j=3;i<3,j>0;i++,j--){
		console.log(i+" "+" "+j);
	}
	</script>
</xmp>
	</div>
	<div>
        <iframe id="preview6"></iframe>
    </div>
</section>

