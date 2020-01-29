<h4>Different Ways to Send/Recive Server Data</h4>
<p>There are 4 way to request server data.</p>
<ol type="1">
	<li>Form Submit</li>
	<li>Through URLs (anchore ag, img tag, link tag etc.)</li>
	<li>Through cookies</li>
	<li>AJAX</li>
</ol>

<h4>On the client side: defining how to send the data through form </h4>
<p> The form element defines how the data will be sent. All of its attributes are designed to let you configure the request to be sent when a user hits a submit button. The two most important attributes are action and method.
</p>

<h5> The action attribute</h5>
<p>This attribute defines where the data gets sent. Its value must be a valid URL. If this attribute isn't provided, the data will be sent to the URL of the page containing the form.</p>
<h5> The action attribute</h5>
<p> This attribute defines how data is sent. The HTTP protocol provides several ways to perform a request; HTML form data can be transmitted via a number of different ones, the most common of which are the GET method and the POST method.</p>

<section>  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:200px;"><xmp><!-- try to add onemore field and see. -->
<form action="http://pioneercoders.com/createUser" method="get">
	First Name :<input type="text" name="first_name" /><br>
	Email  :<input type="email" name="email" /><br>
	Password  :<input type = "password" name="pwd" /><br>
	Mobile  :<input type="text" name="mobile" /><br>	
	<input type="submit"/>
</form></xmp>
	</div>
	<div>
        <iframe id="preview"></iframe>
    </div>
</section>

<h4>Sending request throught Anchore tag </h4>
<section>  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview1',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:200px;"><xmp><!-- try to add onemore field and see. -->
<a href="http://pioneercoders.com/retrieveUser?id=1&method=get"> Retrive user data</a> </xmp>
	</div>
	<div>
        <iframe id="preview1"></iframe>
    </div>
</section>

