<p> The web based applications are dependent on client server architecture irrespective of programming language.</p>

<p> A client (usually a Web browser) sends a request to a server (most of the time a web server like Apache, Nginx, IIS, Tomcat, etc.), using the HTTP protocol. The server answers the request using the same protocol. </p>

@IMG_START@NODEJS/client-server/png@IMG_END@

<p> the server contains set of files(html, css, js, img and videos etc) and data(data from db) to server the client request.</p>

<h4>What is HTTP?</h4>
<p> HTTP, the Hypertext Transfer Protocol, is the application-level protocol that is used
to transfer data on the Web. </p>

<h4> How Does HTTP Work?</h4>
<p> HTTP Is a request-response protocol. For example, a Web browser initiates a request to a server, typically by opening a TCP/IP connection. 
The request itself comprises</p>
<ul>
 <li> a request line,</li>
 <li> a set of request headers</li>
 <li> an entity.</li>
</ul>
<p>The server sends a response that comprises</p>
<ul>
  <li>a status line,</li>
  <li>a set of response headers</li>
  <li>an entity. </li>
</ul>

<h4> Different types of HTTP requests</h4>

<p> There are 9 types of HTTP requests/method. but we mostly use GET and POST methods. </p>
<h5>GET: </h5>
<p> Requests data from a specified resource. </p>
<p> Request Formate: /AppName/retrieveUser?id=1&name=krishna</p>

<h5>POST: </h5>
<p>submits data to be processed (e.g., from an HTML form) to the identified resource. The data is included in the body of the request. This may result in the creation of a new resource or the updates of existing resources or both. </p>
<p> Request Formate: /AppName/createUser</p>

<p>So essentially GET is used to retrieve remote data, and POST is used to insert/update remote data.</p>



