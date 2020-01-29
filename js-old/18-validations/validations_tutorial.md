<p>Validation is knowthing but checking the user data what ever they entered to the form fields like name,emailid.</p>
<p>Validation is simply verifying the user provided data should be proper formate or Not.</p>

<h4>What is form validation</h4>
<p>Go to any popular site with a registration form, and you will notice that they give you feedback when you don't enter your data in the format they are expecting. You'll get messages like:</p>
 <ul>
	<li>1). "This field is required" (you can't leave this field blank)</li>
	<li>2). Password should not be more than 8 character's</li>
	<li>3). "Please enter a valid e-mail address" (the thing you've entered doesn't look like a valid e-mail address)</li>
	<li>4). MobileNo should be 10 digits only</li>
</ul>
<p>This is called form validation when you enter data the web application checks it to see if it is correct. If so, it allows it to be submitted to the server and (usually) saved in a database; if not, it gives you error messages to explain what you've done wrong (provided you've done it right). form validation can be implemented in a number of different ways.</p>
<h4>Different types of form validation</h4>
<p>There are different types of form validation that you'll encounter on the web:</p>
<p><b>Client-side validation</b> is validation that occurs in the browser, before the data has been submitted to the server. This is more user-friendly than server-side validation as it gives an instant response. This can be further subdivided:
	<ul>
		<li>1). JavaScript validation is coded using JavaScript. It is completely customizable.</li>
		<li>2). Built in form validation is done with HTML5 form validation features, and generally doesn't require JavaScript. This has better preformance, but it is not as customizable.</li>
	</ul>
</p>
	
<p><b>Server-side validation</b> is validation that occurs on the server, after the data has been submitted server-side code is used to validate the data before it is put into the database, and if it is wrong a response is sent back to the client to tell the user what went wrong</p>
<p>In the real world, developers tend to use a combination of client-side and server-side validation, to be on the safe side.</p>
<h4>Example: 1</h4>
@CODE_START@@HTML@<html>
<body>
<script>  
function validateform(){  
var name=document.myform.name.value;  
var password=document.myform.password.value;  
  
if (name==null || name==""){  
  alert("Name can't be blank");  
  return false;  
}else if(password.length<6){  
  alert("Password must be at least 6 characters long.");  
  return false;  
  } else{
	alert("Entered data is valid only..")
}
}  
</script>  
<body>  
<form name="myform" method="post" action="" onsubmit="return validateform()" >  
Name:     <input type="text" name="name"><br/>
Password: <input type="password" name="password"><br/>  
<input type="submit" value="register">  
</form>  
</body>
</html>@CODE_END@
<div class="min-height-50" id="jsval1"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsval1','js')">Try Yourself</button></div>
<h4>Example: 2</h4>
@CODE_START@@HTML@<html>
<head>
<title>Form Validation Example</title>
<script type="text/javascript">
function formValidator()
{
var nm=document.forms["form1"]["name"].value;
var em = document.forms["form1"]["email"].value;
var atpos = em.indexOf("@");
var dotpos = em.lastIndexOf(".");
var mn = document.forms["form1"]["mob"].value;
var mobNumLen = document.forms["form1"]["mob"].value.length; 
if(nm == "" || nm == null)
{
alert( "Name Field must not be empty" );
document.form1.name.focus() ;
return false;
} 
if(em == null || nm=="")
{
alert("Email field must not be empty");
document.form1.email.focus();
return false;
} 
if (atpos<1 || dotpos<atpos+2 || dotpos+2>=em.length)
{
alert("Enter proper e-mail address");
document.form1.email.focus();
return false;
}

if(mn == "" || mn == null || isNaN(mn) ||
mn.length < 10 || mn.length >10 )
{
alert( "Mobile Number must be in the format ##### and of minimum 10 digits" );
document.form1.mob.focus() ;
return false;
} 
return( true );

}
</script>
<body>
	<form action="success.html" name="form1"
		onsubmit="return formValidator();">
		<table border="1">
			<tr>
				<td>Name</td>
				<td><input type="text" name="name" /></td>
			</tr>
			<tr>
				<td>EMail</td>
				<td><input type="text" name="email" /></td>
			</tr>
			<tr>
				<td>Mobile Number</td>
				<td><input type="text" name="mob" /></td>
			</tr>
			<tr>
				<td></td>
				<td><input type="submit" value="Submit" /></td>
			</tr>
		</table>
	</form>
</body>
</html>@CODE_END@
<div class="min-height-50" id="jsval2"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsval2','js')">Try Yourself</button></div>
