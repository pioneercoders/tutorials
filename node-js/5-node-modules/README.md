<h4>Node.js Module</h4>
<p><b>Module</b> is a collection of functions or methods which are included in our applications(same like as javascript libraries).</p>
<h4>Node.js Built-in modules</h4>
<p>Node.js has built-in modules</p>
<table class="pc-table">
	<tr>
		<th>Module</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>http</td>
		<td>To make Node.js act as an HTTP server</td>
	</tr>
	<tr>
		<td>https</td>
		<td>To make Node.js act as an HTTPS server</td>
	</tr>
	<tr>
		<td>path</td>
		<td>To handle the file paths.</td>
	</tr>
	<tr>
		<td>fs</td>
		<td>Used for handling file system.</td>
	</tr>
	<tr>
		<td>net</td>
		<td>To create servers and clients</td>
	</tr>
	<tr>
		<td>os</td>
		<td>Provides information about the operation system</td>
	</tr>
	<tr>
		<td>url</td>
		<td>To parse URL strings</td>
	</tr>
	<tr>
		<td>stream</td>
		<td>To handle streaming data</td>
	</tr>
	<tr>
		<td>querystring</td>
		<td>To handle URL query strings</td>
	</tr>
	<tr>
		<td>dns</td>
		<td>To do DNS lookups and name resolution functions</td>
	</tr>	
</table>
<h4>Including Modules into application</h4>
<p>To include the modules into the application, <b>require()</b> function is used.</p>
<h4>Example for including http module</h4>
<section>  
    <div id="nodeHellowWorldEditor" ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'java', previewId:'preview1',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	var http = require('http');
	</div>
</section>
<p>http module is used for creating server.</p>
<h4>Example to create a server</h4>
<section>  
    <div id="nodeHellowWorldEditor" ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'java', previewId:'preview2',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	var http = require('http');
	http.createServer(function(req,res){
		res.writeHead(200,{'Content-Type':'text/html'});
		res.end("Hellow World.")
	}).listen(8080);
	</div>
</section>
<!-- @CODE_START@@HTML@var http = require('http');
http.createServer(function(req,res){
	res.writeHead(200,{'Content-Type':'text/html'});
	res.end("Hellow World.")
}).listen(8080);
@CODE_END@ -->
<h4>Creating custom module</h4>
<p>we will create a module which will return the string("Hellow World!")</p>
<section>  
    <div id="nodeHellowWorldEditor" ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'java', previewId:'preview3',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	exports.myString = function(){
		return "Hellow World!";
	}
	</div>
</section>
<!-- @CODE_START@@HTML@exports.myString = function(){
	return "Hellow World!";
}
@CODE_END@ -->
<p>save the above code with name<b>myfile.js</b></p>
<p><b>exports</b> keyword is to make the properties and methods are available outside module file.</p>
<h4>Including custom module</h4>
<section>  
    <div id="nodeHellowWorldEditor" ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'java', previewId:'preview4',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	var http = require('http');
	var text = require('./myfile');
	http.createServer(function(req,res){
	res.writeHead(200,{'Content-Type':'text/html'});
	res.write(text.myString);
	res.end()
	}).listen(8080);
	</div>
</section>
<!-- @CODE_START@@HTML@var http = require('http');
	var text = require('./myfile');
	http.createServer(function(req,res){
	res.writeHead(200,{'Content-Type':'text/html'});
	res.write(text.myString);
	res.end()
}).listen(8080);
@CODE_END@ -->
<p>save above code with name <b>run.js</b></p>
<p><b>./</b> indicates that the <b>myfile.js</b> in the same location where <b>run.js</b> is located.(<b>both files are in same directory</b>).</p>
