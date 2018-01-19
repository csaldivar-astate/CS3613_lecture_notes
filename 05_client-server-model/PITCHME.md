# Client-Server Architecture

---

## Client-Server Requests

<!-- .element: class="center" -->
![](assets/images/client-server-http.png "Client-Server Request")

1. Client initiates the request
    * request travels to Server over network
    * Server receives the request; performs actions  
2. Server sends its response
    * response travels to Client over network
    * Client receives the response; displays(?) result  
3. <span style="color: grey;">Repeat ... </span>

---

## DNS & HTTP

* **DNS** : Domain Name System
    * provides translation from web URL to IP address.
    * we don't have to worry about this layer (for now)
* **HTTP** : HyperText Transfer Protocol
    * protocol that governs the way WWW requests are structured
    * we **do** need to know a little about this

---

## HTTP Requests

It's all text.<sup style="font-size: 50%">TM</sup>  Requests are plain-text, but must follow the protocol's strict format rules:
```text
Method <SP> Request-URI <SP> HTTP-Version <CRLF>
[<HEADER LINE><CRLF>]*
<CRLF>
[<MESSAGE BODY>]
```

<small style="font-size: 90%">
Where `<SP>` is whitespace, `<CRLF>` is the sequence `\r\n`, `Request-URI` is the URL, `HTTP-Version` is usually (currently) HTTP/1.1<sup>\*</sup>, and `Method` specifies the semantic _action_ that is being requested.<br>
Methods specify things like "GET a document", or "POST this new blog article".
</small>
<small>http://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html</small>

<small><sup>*</sup>&nbsp; HTTP version 2 is rolling out...</small>

---

### Most Common HTTP Request Methods

<small style="font-size: 92%">

* **`GET`** : Requests a representation of the specified resource.
* **`POST`** : Requests that the server accept the entity enclosed in the request as a new subordinate of the web resource identified by the URI.
* **`PUT`** : Requests that the enclosed entity be stored under the supplied URI.
* **`DELETE`** : Deletes the specified resource.
* **`OPTIONS`** : Returns the HTTP methods that the server supports for the specified URL.
* **`PATCH`** : Applies partial modifications to an existing resource.

</small>
<small>http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol</small>

---

<!-- .slide: data-background="assets/images/white_cloud.jpg" -->

### Example `GET` Request

To retrieve the URL: <tt>https://wiki.cs.astate.edu/index.php/Main_Page</tt>    
First:  Open a socket to <tt>https://wiki.cs.astate.edu</tt> on port 443...  Then send the following text:
```http
GET /index.php/Main_Page HTTP/1.1
Host: wiki.cs.astate.edu
[blank line required here]
```

If all goes well, the server will reply:
<small>

```http
HTTP/1.1 200 OK
Date: Thu, 04 Jun 2015 13:51:31 GMT
Server: Apache/2.2.22 (Ubuntu)
X-Powered-By: PHP/5.3.10-1ubuntu3.15
Content-language: en
Vary: Accept-Encoding,Cookie
X-Vary-Options: Accept-Encoding;list-contains=gzip,Cookie;string-contains=wikidbToken;string-contains=wikidbLoggedOut;string-contains=wikidb_session
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Cache-Control: private, must-revalidate, max-age=0
Last-Modified: Tue, 27 Aug 2013 22:01:48 GMT
Transfer-Encoding: chunked
Content-Type: text/html; charset=UTF-8

<< lots of HTML here... >>
```
</small>

---

## HTTP Response Codes
The server sends a _response code_ that tells the client how successful the requested action was. From the previous example:
```http
HTTP/1.1 200 OK
```

Some common codes are listed below:

```asciidoc
200  OK                    403  Forbidden
300  Multiple Choices      404  Not Found
301  Moved Permanently     410  Gone
302  Found                 500  Internal Server Error
304  Not Modified          501  Not Implemented
307  Temporary Redirect    503  Service Unavailable
400  Bad Request           550  Permission denied
401  Unauthorized
```

<small>http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html</small>

---

## HTTP Requests

**Good News!**  We don't usually have to hand-code the HTTP requests; most languages have an HTTP library that does it for us.

We _will_ need to be aware of the different request _methods_.  The entire concept of how "cloud" APIs work is based on these.     
Our server-side controller will respond to requests differently depending on which method is specified.

**Bad News**  Things like _asynchronous background updates_ may require us to  dive into the details of a request.  But even then, there is plenty of information available online.


---

<!-- .slide: data-background="assets/images/cloud-computing-hands.jpg" -->
<div style="background-color: rgba(255,255,255, 0.65); padding: 1.5em; border-radius: .75em;">

<h2> Resources </h2>

<p><b>Reference</b></p>

<p><a href=http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol>http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol</a></p>
<p><a href=http://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html>http://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html</a></p>
<p><a href=http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html>http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html</a></p>

</div>
