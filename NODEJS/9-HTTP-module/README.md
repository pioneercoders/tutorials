<h4>HTTP Module</h4>
<p>HTTP is a built in module in node. Using http we can communicate with servers.</p>
<p>HTTP allows the node.js to transfer the data.</p>
<p><b>require()</b> function is to include the modules in node.js</p>
<section>  
    <div  ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'javascript', previewId:'preview1',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:50px;"><!-- Try change href value and see -->
	var http = require('http');
	</div>
</section>
<h4>Create the Server</h4>
<p>Any node web server application will at some point have to create a web server object. This is done by using createServer.</p>
<section>  
    <div  ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'javascript', previewId:'preview2',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	var http = require('http');
	const server = http.createServer(function(request, response){
	  // write your code here
	});
	</div>
</section>
<p>The function that's passed in to createServer is called once for every HTTP request that's made against that server, so it's called the request handler.</p>
<section>  
    <div  ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'javascript', previewId:'preview3',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	var http = require('http');
	const server = http.createServer(function(request, response){
	  // write your code here
	}).listen(8080);
	</div>
</section>
<p>In order to actually serve requests, the <b>listen()</b> method needs to be called on the server object. In most cases, all you'll need to pass to listen is the port number you want the server to listen on.</p>
<h3>HTTP Header</h3>
<p>when we made an request to the server, depending on request server will return response. If this response is displayed as HTML, we need to set the <b>content-type</b> in the header.</p>
<section>  
    <div  ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'javascript', previewId:'preview4',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:170px;"><!-- Try change href value and see -->
	var http = require('http');
	http.createServer(function (req, res) {
	  res.writeHead(200, {'Content-Type': 'text/html'});
	  res.write('Hello World!');
	  res.end();
	}).listen(8080);
	</div>
</section>
<p><b>req</b> represents request from the client and <b>res</b> is the response from the server.</p>
<p><b>200 status </b>in the above code indicates that all is OK, and the content type as <b>text/html</b></p>
<h4>Read the Query String</h4>
<p><b>req</b> will be sent from client(browser). <b>req</b> is an object which contains the property called <b>url</b>. <b>url</b> will holds the url that comes after domain name. </p>
<h4>Example</h4>
<section>  
    <div  ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'javascript', previewId:'preview5',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	var http = require('http');
	http.createServer(function (req, res) {
	  res.writeHead(200, {'Content-Type': 'text/html'});
	  res.write(req.url);
	  res.end();
	}).listen(8080);
	</div>
</section>
<h4>Output</h4>
@IMG_START@NODEJS/nodeurl/png@IMG_END@
@IMG_START@NODEJS/nodeurl2/png@IMG_END@
<p>we can observe from above output that after domain name we have urls <b>users and list</b></p>
<h4>Split the Query String</h4>
<h4>Example</h4>
<section>  
    <div  ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'javascript', previewId:'preview6',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	var http = require('http');
	http.createServer(function (req, res) {
	  res.writeHead(200, {'Content-Type': 'text/html'});
	   var qùeryString = url.parse(req.url, true).query;
  		var txt = qùeryString.studentname + " " + qùeryString.studentid;
	 	 res.end(txt);
	}).listen(8080);
	</div>
</section>
<h4>URL</h4>
@CODE_START@@HTML@http://localhost:8080/?studentname=pc&studentid=234@CODE_END@	
