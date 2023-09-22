# Glider tests

#### (1)Diagnose a site or page with poor performance
Diagnosing a website or page with poor performance entails a systematic approach to identify bottlenecks and issues affecting speed and usability. Here's a step-by-step guide to help you diagnose performance issues:

Initial Assessment:

Open the page in different browsers and devices to check if the problem persists consistently.
Note the exact scenarios where the performance lags, such as during page load, while scrolling, during interactions, etc.
Use Performance Analysis Tools:

Browser Developer Tools: Both Chrome and Firefox have built-in developer tools to measure website performance. Chrome's Lighthouse can generate a detailed report on performance, accessibility, and more.
Web-based Tools: Websites like GTmetrix, Pingdom, and WebPageTest give insights into page load times and optimization recommendations.
Identify Specific Issues:

Large Media Files: Large images, videos, or other media can significantly slow down page loading.
Too Many HTTP Requests: Multiple scripts, stylesheets, images, or third-party resources can cause excessive HTTP requests.
Unoptimized Code: Bulky or outdated JavaScript libraries, inline styles, or excessive DOM elements can impact performance.
Server Response Time: A slow server response can be due to underpowered hosting, lack of caching, or server location.
Check for Third-party Scripts: Advertisers, trackers, or other third-party scripts can slow down your website.

Check Content Delivery Network (CDN): If you're using a CDN, ensure it's correctly configured and optimized for your content.

Responsive Design Issues: Ensure that media queries or adaptive designs are not causing excessive resource usage on specific devices.

Look for JavaScript Issues:

Blocking JS: JavaScript that blocks rendering can delay page visibility.
Unoptimized Libraries: Using outdated or overly large libraries.
Excessive DOM Manipulations: Constantly updating the DOM can cause lag in interactions.
Server and Hosting:

Hosting Plan: Ensure your hosting plan is adequate for your site's traffic.
Database Optimization: Slow database queries can drastically affect site performance, especially for content management systems.
Server-side Caching: Use technologies like Memcached or Varnish for caching content.
Check for HTTPS Overhead: Implementing SSL can add some overhead, especially if not configured correctly.

Analyze Mobile Performance: Many users access websites on mobile. Use tools like Google's Mobile-Friendly Test to diagnose mobile-specific issues.

Content Management System (CMS): Some CMS plugins or themes can introduce performance issues.

Check for Redirects: Excessive redirects, especially 301 or 302, can delay page load.

Optimize CSS and JS: Minify and concatenate files to reduce size and number of requests.

Review HTTP Headers and Caching:

Ensure assets have correct cache headers.
Use HTTP/2 or HTTP/3 if possible to reduce the overhead of multiple connections.
Web Fonts: Limit the number of font weights and styles. Use font-display: swap to ensure text remains visible during web font loading.
After identifying specific issues, focus on optimizing and rectifying each bottleneck. Monitor performance regularly and keep your site's components updated for best results.

#### (2)In Angular , How the structure of an HTML document impacts screen readers
In Angular applications, just like any web application, the structure of the HTML document significantly impacts how screen readers interpret and present content to users. Angular's dynamic nature adds some nuances to this:

Semantic Elements: Just like with plain HTML, semantic tags in Angular help screen readers understand the structure and meaning of content.

Examples: <header>, <nav>, <main>, <article>, <section>, <aside>, <footer>
Angular Components: Components are the building blocks of Angular apps. When defining components, it's essential to ensure that the rendered HTML is accessible.

Use appropriate roles and ARIA attributes when necessary.
Avoid unnecessary container elements that can clutter the structure without adding semantic value.
Dynamic Content: Angular apps often update content dynamically.

Use aria-live regions for content that changes often, so screen readers can announce changes.
Manage focus when new views or modals appear to guide the screen reader user through the app seamlessly.
Routing & Navigation: Angular's Single Page Application (SPA) nature means traditional page reloads are absent.

Manage focus when navigating between routes to ensure screen readers read the new content.
Use meaningful titles for routes to indicate context changes.
Forms: Angular provides a powerful forms API.

Use <label> elements with form controls.
Utilize aria-describedby for error messages and hints.
For custom form controls, use roles and ARIA attributes to ensure they're accessible.
Animations & Transitions: While they can be visually appealing, animations can be confusing for screen reader users.

Provide options to disable animations.
Ensure transitions do not interrupt screen reader announcements.
Lazy Loading & Virtual Scrolling: Both techniques can affect screen reader experiences.

For lazy loading, ensure that newly loaded content is accessible and announced by the screen reader if necessary.
For virtual scrolling, be cautious as this technique can sometimes confuse screen readers due to DOM elements being added and removed dynamically.
Use of ARIA: While Angular offers tools to make applications interactive, sometimes it's necessary to use ARIA to enhance accessibility.

Only use ARIA when semantic HTML isn't sufficient.
Ensure ARIA roles and attributes are used correctly.
Keyboard Navigation: Ensure all interactive elements are keyboard-accessible and that focus order is logical. This impacts both screen reader users and those who rely solely on keyboards.

Testing: Always test Angular apps with real screen readers (e.g., NVDA, JAWS, VoiceOver) to understand the user experience.

Automated accessibility testing tools (like axe-core) can help catch issues, but manual testing is crucial.
In summary, while Angular provides tools and methodologies for building dynamic web applications, developers must be diligent in ensuring that the resulting structure is logical, meaningful, and accessible for screen reader users. Properly structured HTML, combined with thoughtful application design, can lead to an inclusive user experience for everyone.
#### (3)Describe what occurs from the time you enter a URL into the browser and from when the page is presented ?
The process that unfolds from the moment you enter a URL into a browser until the page is fully presented is quite complex. Here's a step-by-step breakdown of this process:

URL Input:

When you type a URL and hit Enter, the browser needs to determine if it's a search query or a URL. If it's a search query, the browser redirects to your default search engine. If it's a URL, the process continues.
Domain Name System (DNS) Lookup:

The browser checks its cache to see if it has a recent IP address for the requested domain. If not:
The OS checks its own cache to see if it has a matching IP.
If the OS doesn’t have a matching IP, a DNS query is made to find the IP address associated with the domain name.
The request is sent to a DNS server, which resolves the domain name to an IP address.
Browser Initiates a TCP Connection:

Using the IP address obtained, the browser establishes a TCP (Transmission Control Protocol) connection with the server. This is achieved using a three-way handshake:
The browser sends a SYN (synchronize) packet.
The server responds with a SYN-ACK (synchronize-acknowledge) packet.
The browser sends an ACK (acknowledge) packet.
Send an HTTP Request:

The browser sends an HTTP (or HTTPS, if secure) request to the web server asking for the desired webpage.
Server Processing:

The server processes the request. If the website uses server-side scripting (like PHP, Python, Ruby, etc.), the server will execute the script and generate the appropriate HTML.
Server Responds:

The server sends back an HTTP response. The response contains a status code (like 200 for OK, 404 for Not Found), headers about the response/data, and the content itself (usually the HTML of the page).
Rendering the Page:

The browser starts rendering the page.
HTML is parsed and the Document Object Model (DOM) is built.
CSS, whether external or inline, is parsed and the CSS Object Model (CSSOM) is built.
The DOM and CSSOM are combined into a render tree.
Layout: The browser calculates the geometry of the render tree elements.
Painting: The render tree is traversed to paint each node.
Executing JavaScript:

JavaScript, whether inline or external, is parsed and executed. JavaScript can modify the DOM and CSSOM, which might require the page to be repainted.
Loading External Resources:

During the process, the browser will also make additional requests for external resources referenced in the HTML, such as images, CSS, JavaScript files, and more. Each of these requires additional HTTP requests.
SSL/TLS for HTTPS:

If the URL is using HTTPS, there's an added layer of SSL/TLS handshaking for a secure connection. This process involves certificate validation and key exchange to encrypt the connection.
Page Displayed:
After all the steps mentioned, the browser finally displays the complete page to the user.
Throughout this process, various optimizations like browser caching, content delivery networks (CDNs), protocol upgrades (like HTTP/2 or HTTP/3), and server-side optimizations can make the process faster and more efficient.
#### (4)Provide some othe available databse options in GCP and when you might use each
Google Cloud Platform (GCP) offers a variety of managed database services tailored to different use cases. Here are some of the primary database options available on GCP, along with scenarios for when you might use each:

Cloud SQL:

Type: Relational Database Management System (RDBMS)
Supported Databases: MySQL, PostgreSQL, SQL Server
Use Cases: Traditional web applications, CRM systems, e-commerce platforms, any workload requiring relational database capabilities.
Cloud Spanner:

Type: Globally distributed, horizontally scalable RDBMS
Use Cases: Global online transaction processing (OLTP) systems, applications requiring strong consistency and high availability at global scale, large-scale e-commerce platforms.
Cloud Bigtable:

Type: NoSQL database service (Wide-column store)
Use Cases: Time-series data, monitoring applications, analytical and operational workloads, IoT applications, and applications requiring low-latency and high-throughput.
Firestore (previously Cloud Firestore):

Type: NoSQL document database
Use Cases: Mobile apps, web applications, serverless architectures, real-time collaboration apps, applications requiring real-time sync.
Firebase Realtime Database:

Type: NoSQL cloud-hosted database (JSON)
Use Cases: Real-time collaboration, syncing data across applications in real-time, building MVPs for mobile or web applications.
Cloud Memorystore:

Type: In-memory data store
Supported Databases: Redis and Memcached
Use Cases: Caching layer for applications, session storage, leaderboards for gaming applications, and real-time analytics.
BigQuery:

Type: Serverless, highly scalable, multi-cloud data warehouse
Use Cases: Analyzing large datasets in real-time, BI (business intelligence) tools integration, machine learning workloads with BigQuery ML.
Cloud Datastore:

Type: NoSQL database service (deprecated in favor of Firestore in Datastore mode)
Use Cases: Web and mobile applications with varying loads and requiring scalability without manual intervention.
Choosing the right database often depends on several factors like data model, scalability requirements, access patterns, geographical distribution of users, consistency requirements, and more. With GCP's range of database options, businesses can pick the solution that best aligns with their use case.

#### (5)Angular what is eager and lazy loading? are there any advantages to one over the other ?
n Angular, eager loading and lazy loading pertain to how Angular modules (and their associated components, directives, and services) are loaded. Both approaches have their own set of advantages.

Eager Loading:
Definition: When an Angular application starts, all the application's modules are loaded immediately.

Advantages:

Initial Setup Simplicity: With eager loading, setting up routing is straightforward since all components and modules are available from the start.
Immediate Availability: After the initial load, navigation between routes/components is typically fast because all components are pre-loaded.
Disadvantages:

Slower Initial Load: The browser must download, parse, and execute the entire application (all modules, components, services, etc.) before the app can become interactive. This can lead to a longer perceived start-up time, especially for large applications.
Lazy Loading:
Definition: Only the necessary modules are loaded when the application starts. Other modules are loaded on-demand, usually as a user navigates to specific routes that require those modules.

Advantages:

Faster Initial Load: The browser only needs to deal with a subset of the application to bootstrap it. This means quicker initial load times, leading to faster Time-to-Interactive (TTI) metrics.
Optimized Bandwidth Usage: Users download only the parts of the application they use. If a user never navigates to a specific module, it won't be loaded, saving bandwidth.
Improved Scalability: As an application grows, lazy loading can prevent the initial bundle from becoming too large.
Disadvantages:

Complexity: Setting up lazy loading requires a bit more configuration in your Angular routes.
Latency on First Access to Lazy-Loaded Modules: The first time a user navigates to a component from a lazy-loaded module, there may be a slight delay as the module is loaded.
Choosing Between Eager and Lazy Loading:
Small Apps: For small applications with minimal modules and components, the advantages of lazy loading might not be as noticeable, making eager loading an acceptable choice.

Large Apps: For larger applications with many modules, especially when not all users will use all modules, lazy loading can significantly enhance the initial loading experience.

User Experience Considerations: If a smooth, immediate navigation experience is a priority after the initial load, eager loading can be beneficial. If improving initial load time is more crucial, then lazy loading is advantageous.

In many modern Angular applications, a combination of both strategies is used: core and commonly used features are eagerly loaded for immediate use, while less-frequently used features are lazy-loaded. This hybrid approach provides a balance between initial load performance and seamless navigation afterwards.

#### (6)Difference between authentication and autherization.

Authentication and authorization are two fundamental concepts in security, but they serve different purposes. Let's break down their definitions and highlight the differences:

Authentication:
Definition: Authentication is the process of verifying the identity of a user, system, or application. It answers the question, "Who are you?"

Common Methods:

Username and Password: The most common method, where users provide a username (or email) and a password.
Multi-Factor Authentication (MFA): Requires the user to provide multiple forms of identification. For instance, in addition to a password, they might receive a code on their phone that they also need to enter.
Biometrics: Uses unique biological characteristics, such as fingerprints, facial recognition, or retinal scans.
Token-based Authentication: After initial authentication, a token is provided to the user, which can be used for subsequent requests without re-entering credentials.
Authorization:
Definition: Authorization is the process of determining what actions, resources, or services a verified identity is allowed to access. It answers the question, "What are you allowed to do?"

Common Methods:

Role-Based Access Control (RBAC): Assigns roles to users, and permissions to roles. A user gets access based on their role.
Access Control Lists (ACL): Specifies which users or system processes are granted access and what operations they can perform on a particular object.
Attribute-Based Access Control (ABAC): Uses attributes (such as department, title, and more) to determine a user's access rights.
Capability-Based Access Control: Grants permissions based on tokens (capabilities) which a user possesses.
Key Differences:
Purpose:

Authentication: Confirms you are who you say you are.
Authorization: Determines what you're allowed to do once your identity is confirmed.
Sequence:

Authentication typically precedes authorization. First, a system determines who you are. Then, it decides what you're allowed to do.
Common Failures:

Authentication: Wrong password, expired credentials, MFA failure.
Authorization: Trying to access a restricted resource, performing an action outside of allowed permissions.
Example:

Authentication: Logging into an email service using your email and password.
Authorization: Once logged in, you might have permissions to read, send, and delete emails but not to configure advanced server settings.
In summary, while both authentication and authorization are closely related and often used in tandem, they address different security concerns: "Who are you?" versus "What are you allowed to do?" respectively.

#### (7)What is CORS ?
the one from which the web page originates. Without CORS, web browsers restrict web pages from making requests to a different domain than the one that served the web page, a principle known as the "same-origin policy."

The same-origin policy is important for security reasons. For example, without it, malicious scripts on Web Page A could request sensitive user data from Web Page B without the user's knowledge. However, there are legitimate scenarios where cross-domain requests are needed. CORS provides a controlled mechanism to allow web pages to make cross-domain requests, bypassing the same-origin policy in a secure manner.

How CORS Works:
Preflight Request: Before making the actual request, the browser may send a preliminary "preflight" request to the server using the HTTP OPTIONS method. This request checks whether the server will allow the actual future request.

Headers: The server communicates its CORS policy to the browser using specific HTTP headers. Some common CORS headers include:

Access-Control-Allow-Origin: Specifies which origins can access the resource.
Access-Control-Allow-Methods: Specifies which HTTP methods are allowed.
Access-Control-Allow-Headers: Specifies which HTTP headers can be used.
Access-Control-Allow-Credentials: Indicates whether or not the browser should include credentials with requests.
Actual Request: If the server permits it (based on the received headers), the browser will make the actual request for the resource.

Server Response: When responding to a CORS request, the server includes the appropriate CORS-related headers to tell the browser if the original request is allowed.

Example:
Imagine a web application loaded from https://webapp.com wants to fetch user data via AJAX from https://api.com/userdata. The browser initiates the request and checks for CORS headers in the response. If api.com returns a response with the header Access-Control-Allow-Origin: https://webapp.com, the browser allows the request. If not, the browser will block the request, and you'll see a CORS-related error in the browser console.

Notes:
For servers to support CORS, specific configurations are usually needed to return the appropriate headers.

There are tools and libraries, like the CORS middleware for Express.js in Node.js, that simplify the implementation of CORS on the server side.

Not all cross-origin requests require a preflight request. "Simple requests," like those using the GET or POST method with specific content types, don't trigger a preflight check. However, requests with methods like DELETE or PUT or those using custom headers typically will trigger a preflight request.

In summary, CORS is a protocol that allows for secure cross-origin requests, giving developers a way to bypass the same-origin policy under specific, controlled circumstances.

#### (8)wirte a typesction function to determine if a given string is a palindrome 



```typescript
function isPalindrome(s: string): boolean {
    // Remove non-alphanumeric characters and convert to lowercase
    const cleanedString = s.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();
    
    // Compare the string with its reverse
    return cleanedString === cleanedString.split('').reverse().join('');
}

// Test the function
console.log(isPalindrome("A man, a plan, a canal, Panama!")); // true
console.log(isPalindrome("racecar")); // true
console.log(isPalindrome("hello"));   // false
```
