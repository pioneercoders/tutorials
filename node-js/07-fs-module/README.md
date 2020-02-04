<h4>fs Module</h4>
<p>fs stands for File System. Node.js includes fs module to access physical file system. The fs module is responsible for all the asynchronous or synchronous file I/O operations.</p>
<h4>File System Module Operations</h4>
<ul>
	<li>Reading Files</li>
	<li>Creating Files</li>
	<li>Updateing Files</li>
	<li>Renaming Files</li>
	<li>Deleting Files</li>
</ul>
<h4>Read Files</h4>
<h5>Syntax</h5>

```javascript
fs.readFile(fileName [,options], callback)
```

<p><b>Parameters</b></p>
<p><b>filename:</b> Full path and name of the file as a string.</p>
<p><b>options:</b> The options parameter can be an object or string which can include encoding and flag. The default encoding is utf8 and default flag is "r".</p>
<p><b>callback:</b> A function with two parameters err and fd. This will get called when readFile operation completes.</p>
<h4>Example Reading File.</h4>
<p>screenshot of <b>myFile.txt</b></p>

![myFiletxt](https://github.com/pioneercoders/pc-tutorials/blob/master/node-js/images/myFiletxt.PNG)

<p><b>Code for reading File</b></p>

```javascript
fs = require('fs')
    fs.readFile(fileName.txt, 'utf8', function (err,data) {
      if (err) {
        return console.log(err);
      }
      console.log(data);
    });
```

<h4>Output</h4>

![readFileOutput](https://github.com/pioneercoders/pc-tutorials/blob/master/node-js/images/readFileOutput.PNG)

<h4>Create Files</h4>
<p>Files can be created using three methods.</p>
<ul>
	<li>fs.appendFile()</li>
	<li>fs.writeFile()</li>
	<li>fs.open()</li>
</ul>
<table class="pc-table">
	<tr>
		<th>Method</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>fs.appendFile()</td>
		<td>This method will append text to existing file. If file does not exist then it will create the new file.</td>
	</tr>
	<tr>
		<td>fs.writeFile()</td>
		<td>replaces the content in specified file. If the file does not exist. It creates the new file.</td>
	</tr>
	<tr>
		<td>fs.open()</td>
		<td> method takes a "flag" as the second argument, if the flag is "w" for "writing", the specified file is opened for writing. If the file does not exist, an empty file is created:</td>
	</tr>
</table>
<h4>fs.append() example</h4>

```javascript
var fs = require('fs');
//append content at the end of the file:
fs.appendFile('DirectoryName\\mynewfile1.txt', ' This is my text.',
function (err) {
	  if (err) throw err;
	  console.log('Updated!');
	});
```

<p>In the above example  we are appending text called <b>Pioneer Coders</b>. to file <b>pcFile</b>. if <b>pcFile doesnot exist it will create the file</b> with file name 'pcFile'</p>
<h4>fs.writeFile() example</h4>

```javascript
fs = require('fs');
fs.writeFile('writeContent.txt', 'write the content to file using this function',
function (err) {
  if (err) return console.log(err);
  console.log('Desktop > writeContent.txt');
	});
```

<h4>Example: creating file using fs.open();</h4>

```javascript
var fs = require('fs');
//create an empty file named mynewfile2.txt:
fs.open('DirectoryName\\mynewfile2.txt', 'w', function (err, file) {
  if (err) throw err;
  console.log('Saved!');
	});
```

<h4>Update Files</h4>
<p><b>File System Update methods</b></p>
<ul>
	<li>fs.appendFile()</li>
	<li>fs.writeFile()</li>
</ul>
<p><b>fs.appendFile()</b> method updates the existing file. It will appends the content at end file that specified</p>
<h4>Example</h4>

```javascript
var fs = require('fs');
//append content at the end of the file:
fs.appendFile('DirectoryName\\mynewfile1.txt', ' This is my text.', function (err) {
  if (err) throw err;
  console.log('Updated!');
	});
```

<h4>fs.writeFile()</h4>
<p><b>fs.writeFile()</b> method replaces the specified file and content:</p>
<h4>Example</h4>

```javascript
var fs = require('fs');
fs.writeFile('DirectoryName\\writeContent.txt', 'write the content to file using this function', 
function (err) {
  if (err) return console.log(err);
  console.log('Desktop > writeContent.txt');
	});
```

<h4>Delete File()</h4>
<p><b>fs.unlinkFile()</b> method used to delete the specified file.</p>
<h4>Example</h4>

```javascript
var fs = require('fs');
fs.unlink('DirectoryName\\mynewfile2.txt', function (err) {
  if (err) throw err;
  console.log('File deleted!');
	});
```

<p>Above example deletes the file <b>pcFile.txt</b>
