# Cloud Basics

---

## What _is_ "The Cloud" Anyway?

<!-- .slide: data-background="assets/images/question_cloud.jpg" -->

---

## What _is_ "The Cloud" Anyway?

* The _Cloud_ is just a buzzword for the Internet.
* A _Cloud Application_ is just an application that runs on a server somewhere that _isn't_ on your local machine.
* Your local machine becomes a _client_, concerned mostly with _UI_.
* "Heavy" processing and data storage concerns are left to the server.

---

## Client-Server Architecture  

<!-- .element class="center" -->
![Clients and a Server](assets/images/serverclient.jpg "Clients and a Server")

Users operate the _client_ machines (outer ring).

_Server_ (center) performs computation and manages long-term storage.

---

## The Server

The _server_ is a computer (or virtual machine) optimized for the necessary computation and storage.

* Often runs Linux or other Gen. Purpose OS.
* Often resides in a large data center somewhere.
    * Managed over the network. (`ssh`)

---

## The Server (process)

There must be a _server process_ running on the server (machine).

* Listens for client requests on well-known port.
    - Ex: Web servers use port 80 (443 for https).
* May directly serve files, or spawn sub-processes that perform computation.
* Examples:
    - static: Apache, IIS, Nginx
    - proxy: Nginx
    - Other: Tomcat 
    - Ad-Hoc (Node.js, Go!)

---

## The Client

Clients are often using a _web browser_ to access the server.

* Browser "speaks" HTTP and HTTPS protocols (and maybe others).
* Browser implements an HTML/CSS display layer.
* Browser can execute scripts in JavaScript (and maybe others).

Clients may also be purpose-built applications (designed only to interact with the application server).

---

## The Client (software)

<small class="center">_Assuming a Web Browser on the client side._</small><br />
The client-side will receive HTML, CSS, and maybe JavaScript documents from the server.

* HTML is the _information_ being presented, marked up with some semantic information.
* CSS is the _style rules_ that the browser should apply when rendering the HTML.
* JavaScript is _executable source code_ that runs in the browser; can do dynamic formatting or more general computation.

---

## HTML

_**H**yper**T**ext **M**arkup **L**anguage_ is the standard markup language used on the web.

* Based on plain-text.
* _Tags_ are added to "explain" semantic information to the renderer.
    - Tags are surrounded with angle brackets:<br /> `<p>This is a paragraph.</p>`.
    - There is usually a matching pair of tags: An _open_ tag and a _close_ tag.
    - Some tags don't require and end tag.  Ex: `<br>`
        + <small>`area`, `base`, `br`, `col`, `embed`, `hr`, `img`, `input`, `keygen`, `link`, `meta`, `param`, `source`, `track`, `wbr`</small>

http://en.wikipedia.org/wiki/HTML

---

### HTML Example

```html5
<!DOCTYPE html>
<html>
  <head>
    <title>Example Page</title>
  </head>
  <body>
    <p>
      This is an example of an HTML document. The whitespace is 
      irrelevant!  You can write so that it is readable in your 
      text editor. Also, <em>it is plain-text</em>.
    </p>
    <ul>
      <li> You can link to a page with an <i>anchor</i> tag: 
           <a href="http://google.com">Google!</a>
      </li>
    </ul>
  </body>
</html>
```

----

### HTML Example

This page's title (in the browser tab, usually) would be "Example Page".

<iframe src="resources/simple_example_page.html"></iframe>

---

### CSS Example

```css
body {
    font-family: Helvetica, 'Sans-Serif';
    font-size: 18px;
    color: #fff0cf;
    background-color: #496b73;
}

a {
    color: #ffd5cf;
}
```

To use it, add the following to the `<head>` section of your HTML:

```html5
<link rel="stylesheet" type="text/css" href="path/to/style.css">
```

----

### CSS Example

Before styling:

<iframe src="resources/simple_example_page.html"></iframe>

After styling:

<iframe src="resources/simple_example_page_styled.html"></iframe>

---

## Links

* HTML5 / CSS
    - <small>https://developer.mozilla.org/en-US/docs/Web/Guide</small>
* CSS
    - <small>http://tympanus.net/codrops/css_reference/</small>
* Experiment:
    - HTML and CSS
        + <small>http://www.cssdesk.com/</small>
    - HTML+CSS+JavaScript
        + <small>https://jsfiddle.net/</small>
* Develop/Deploy
    - CodeAnywhere (Also serves as an online IDE!)
        + <small>https://http://codeanywhere.com</small>
