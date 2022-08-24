---
title: "Notes — Web Pentest : Day 002"
date: 2022-08-23 22:20:00 +0530
categories: [Red Team Notes,Web]
tags: [Web, Basics]
image: /assets/img/Posts/RedNotes/web100/was-ist-http-t.jpg 
---

>This is the second day of my 100 day of web hacking journey, beginner to hacker
>Day 2 i decided to expound more on some of the client and server technology http methods and status codes

### 1. HTML - Hypertext markup language - Client-side
HTML or hypertext markup language is one of the "markup" languages as the name implies. It was designed to be displayed in a web browser. Having a basic understanding of HTML is important for web hacking so having a basics in the language is a plus.

Every HTML document will look like this:

```html
<html>

 <head></head>

 <body></body>

</html>
```
  
One thing about HTML is that its a very fault tolerant language and the browser automaticaly corrects any errors.
For an example when you create an html file named "winter-day2.html" with any random value, the browser will open and display the text just fine this is because the browser add the structures for you. 


### 2. CSS - Cascading style sheets - Client-side
HTML on its own is already functional as it is, but if you need to pimp your your newly website HTML wont cut it and thats where CSS comes in. Casscading Style Sheet as its name implies is used to style the webpage.Basically CSS is the makeup of the website

```css
body {

  font-size: 10pt;

  font-family: Verdana, Geneva, Arial, Helvetica, sans-serif;

  color: black;

  line-height: 14pt;

  padding-left: 5pt;

  padding-right: 5pt;

  padding-top: 5pt;

}

```
  
### 3. JavaScript - Client-side, with possibility of server-side through nodeJS for example

Finally after creating our website and styling it we might need to add some functionalities or even annimations i.e interactive elements such as an image carousel or a distance calculator. This is where HTML and CSS fall short and where JS comes in. This powerful scripting language looks like nothing like its namesake java. Where Java needs a VM for example, javascript is perfectly content by running in your browser and there have even been several libraries created for game development. 

>Because javascript is so powerful, attackers will often try to leverage it to do things like steal session cookies or CSRF tokens. Anyone that wants to get serious about XSS should have at least a surface-level understanding of javascript and be very willing to learn while hacking. Of course, most javascript concepts can be taught fairly easily but to intuitively debug a script that is not displaying an XSS attack vector, is a different story.

```html
<script>alert()</script>
```

### 4. PHP/ASPX/Python/NodeJS/... - Back-end systems

Now that we have a nice-looking functional website, we want to bring some of the logic to the back-end to ensure we can control it better and to form an abstraction layer for certain security-sensitive processes. This layer basically servers to act in between what the users see and how the data is processed before it reaches the UI. What these technologies can still do however is display and manipulate what the final HTML of a webpage will look like when it is served to a user. This might be different for every user, for example, a user might only be able to see their own data after logging in and no data when not logged in.

**Client Side**

```html
<form action="32.php" method="GET">

  <div>

    <label for="say">What greeting do you want to say?</label>

    <input name="say" id="say" value="Hi">

  </div>

  <div>

    <button>Send my greetings</button>

  </div>

</form>

  
```

**Server side** 
```php
<?php


if(isset($_GET['say']) && (str_contains($_GET['say'],'alert') || str_contains($_GET['say'],'confirm') || str_contains($_GET['say'],'prompt')) ){

        echo htmlentities($_GET['say']);

}else{

        if(isset($_GET['say'])){

                echo $_GET['say'];

        }

}
  
?>

```

### 5. Storage - Client-side and server-side storage

#### Cookies
Now that we have UI and logic of our website, we need away to store data localy or remotely. Localy(on the user machine) we can often find cookies. These cookies contain little snippets of information such as the session token, a search term that might need to be remembered, or a group. 

These cookies are set and passed back to the server in the header of a request/response. When they are set, they will have 4 possible flags which can each be true or false. These flags serve to increase security but they are not the only defenses. These flags however have made cookie stealing less prevalent and XSS hunters have had to adapt. 

#### Local/remote file storage

Besides the storage on the client, we can store things on the server as well for persistence and security (Can you imagine the security nightmare if everyone held onto their balance at a bank account via client-side storage?). This can either be done by inserting the data into a file or database. When the data is stored on a local file, of course, we need to take great care to encrypt this file and to protect it properly. This is not easy as usually many different users of different privilege levels exist which might have unexpected results on the file storage security.

Of course, remote storage systems are not spared from this complexity and they have the added issue of having to take data transfer over the network into account.

#### Local/remote database systems

Just as we can make use of local or remote file storage systems, we can also use database systems such as MySQL or MariaDB. These take away a lot of the complexity that comes with securing the data and lock it behind proper access control.

## 6. HTTP methods

HTTP supports multiple methods for accessing a resource. In the HTTP protocol, several request methods allow the browser to send information, forms, or files to the server. These methods are used, among other things, to tell the server how to process the request we send and how to reply.


<table>
<thead>
<tr>
<th><strong>Method</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>GET</code></td>
<td>Requests a specific resource. Additional data can be passed to the server via query strings in the URL (e.g. <code>?param=value</code>).</td>
</tr>
<tr>
<td><code>POST</code></td>
<td>Sends data to the server. It can handle multiple types of input, such as text, PDFs, and other forms of binary data. This data is appended in the request body present after the headers. The POST method is commonly used when sending information (e.g. forms/logins) or uploading data to a website, such as images or documents.</td>
</tr>
<tr>
<td><code>HEAD</code></td>
<td>Requests the headers that would be returned if a GET request was made to the server. It doesn't return the request body and is usually made to check the response length before downloading resources.</td>
</tr>
<tr>
<td><code>PUT</code></td>
<td>Creates new resources on the server. Allowing this method without proper controls can lead to uploading malicious resources.</td>
</tr>
<tr>
<td><code>DELETE</code></td>
<td>Deletes an existing resource on the webserver. If not properly secured, can lead to Denial of Service (DoS) by deleting critical files on the web server.</td>
</tr>
<tr>
<td><code>OPTIONS</code></td>
<td>Returns information about the server, such as the methods accepted by it.</td>
</tr>
<tr>
<td><code>PATCH</code></td>
<td>Applies partial modifications to the resource at the specified location.</td>
</tr>
</tbody>
</table>
<p>The list only highlights a few of the most commonly used HTTP methods. The availability of a particular method depends on the server as well as the application configuration. For a full list of HTTP methods, you can visit this <a href="[https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods](view-source:https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)">link</a>.</p>
<div class="card bg-light">
<div class="card-body">
<p class="mb-0"><b>Note:</b> Most modern web applications mainly rely on the <code>GET</code> and <code>POST</code> methods. However, any web application that utilizes REST APIs also rely on <code>PUT</code> and <code>DELETE</code>, which are used to update and delete data on the API endpoint, respectively.</p>
</div>
</div>

## 7. Response Codes
<p>HTTP status codes are used to tell the client the status of their request. An HTTP server can return five types of response codes:</p>
<table>
<thead>
<tr>
<th><strong>Type</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>1xx</code></td>
<td>Provides information and does not affect the processing of the request.</td>
</tr>
<tr>
<td><code>2xx</code></td>
<td>Returned when a request succeeds.</td>
</tr>
<tr>
<td><code>3xx</code></td>
<td>Returned when the server redirects the client.</td>
</tr>
<tr>
<td><code>4xx</code></td>
<td>Signifies improper requests <code>from the client</code>. For example, requesting a resource that doesn't exist or requesting a bad format.</td>
</tr>
<tr>
<td><code>5xx</code></td>
<td>Returned when there is some problem <code>with the HTTP server</code> itself.</td>
</tr>
</tbody>
</table>
<p>The following are some of the commonly seen examples from each of the above HTTP method types:</p>
<table>
<thead>
<tr>
<th><strong>Code</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>200 OK</code></td>
<td>Returned on a successful request, and the response body usually contains the requested resource.</td>
</tr>
<tr>
<td><code>302 Found</code></td>
<td>Redirects the client to another URL. For example, redirecting the user to their dashboard after a successful login.</td>
</tr>
<tr>
<td><code>400 Bad Request</code></td>
<td>Returned on encountering malformed requests such as requests with missing line terminators.</td>
</tr>
<tr>
<td><code>403 Forbidden</code></td>
<td>Signifies that the client doesn't have appropriate access to the resource. It can also be returned when the server detects malicious input from the user.</td>
</tr>
<tr>
<td><code>404 Not Found</code></td>
<td>Returned when the client requests a resource that doesn't exist on the server.</td>
</tr>
<tr>
<td><code>500 Internal Server Error</code></td>
<td>Returned when the server cannot process the request.</td>
</tr>
</tbody>
</table>

Thats the end of day 002 ... see you tomorrow