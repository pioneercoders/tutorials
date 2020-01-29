<h4>NPM(Node Package Manager)</h4>
<p>npm is a package manager for the JavaScript programming language.</p>
<p>npm is Node Package Manager for downloading node.js packages or modules.</p>
<p>NPM comes bundled with Node.js installables after v0.6.3 version.</p>
<p>nmp providies main functionalities like</p>
	<ul>
		<li>Provides online repositories for node.js modules.</li>
		<li>Command line utility to install Node.js packages, do version management and dependency management of Node.js packages.</li>
	</ul>
<h4>Verify wheather npm is installed or not?</h4>
<p>by default npm will be automatically installed when node.js is installed (npm will be installed if and only if node.js version is greater than <b>0.6.3</b>)</p>
<p>to verify the npm, open command prompt type bellow command.</p>
@CODE_START@ npm -version
@HTML@@CODE_END@
<p>@IMG_START@NODEJS/npmversion/png@IMG_END@</p>
<p>In the above screenshot 3.10.10 is the npm version.</p>
<p>There are two types npm installation are there to install the required dependencies.</p>
	<ul>
		<li>Global installation.</li>
		<li>Local installation.</li>
	</ul>
<h4>Global installation of node modules</h4>
<p>Globally installed packages/dependencies are stored in system directory. These dependencies can be used in CLI(Command Line Interface) but cannot be imported using <b>require()</b> function into node application directly.</p>
<h4>Syntax for Global installation</h4>
@CODE_START@ npm install <Module Name> -g
@HTML@@CODE_END@
<p>suppose we want install express js globally. use below command.</p>
@CODE_START@ npm install express -g
@HTML@@CODE_END@
<p>Type the above command in CLI and press enter.</p>
<p>@IMG_START@NODEJS/npmExpressinstall/png@IMG_END@</p>
<p>express module will be installed globally.</p>
<h4>local installation</h4>
<p>node packages/modules will install in the local directory where the node.js application is present.</p>
<h4>Syntax</h4>
@CODE_START@ npm install <Module Name>
@HTML@@CODE_END@
<h4>Example: Installing express node package locally.</h4>
<p>First change the directory in the CLI to directory where node.js application is present. Suppose if the node.js application on desktop. then change directory using command(<b>cd Desktop</b>).</p>
@CODE_START@ npm install <Module Name>
@HTML@@CODE_END@
<p>@IMG_START@NODEJS/localnpmExpressinstall/png@IMG_END@</p>
<p>After executing above command. All dependencies and express will be downloaded from repository.</p>
<h4>Example</h4>
<p>Converting text to upper-case using upper-case package.</p>
<p><b>installing upper-case using npm</b></p>
@CODE_START@ npm install upper-case
@HTML@@CODE_END@
<p>@IMG_START@NODEJS/upper-case-package/png@IMG_END@</p>
<p>Code</p>
<section>  
    <div  ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'java', previewId:'preview1',
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:150px;"><!-- Try change href value and see -->
	 var http = require('http');
	var uc = require('upper-case');
	http.createServer(function (req, res) {
	    res.writeHead(200, {'Content-Type': 'text/html'});
	    res.write(uc("Pioneer Coders."));
	    res.end();
	}).listen(9090);
	</div>
</section>
<h4>Output</h4>
<p>@IMG_START@NODEJS/upper-case/png@IMG_END@</p>
