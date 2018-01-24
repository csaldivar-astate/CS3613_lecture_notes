# Cloud App Design
## Featuring: The MVC Pattern

---

## Model-View-Controller

The _Model-View-Controller_ (MVC) design pattern focuses on the _separation of concerns_ of an application into three parts:

<!-- .element: style="width: 9em; position: relative; float: right; display: block;" -->
!["MVC-Process" by RegisFrey - Own work. Licensed under Public Domain via Wikimedia Commons - http://commons.wikimedia.org/wiki/File:MVC-Process.svg#/media/File:MVC-Process.svg](https://cdn.rawgit.com/jcausey-astate/CS3613_lecture_notes/master/assets/images/MVC-Process.svg "MVC-Process")
<small style="width: 17em; font-size: 95%;">

* Model
    - encapsulate data and basic behaviors
* View
    - presents information to the user
* Controller
    - tie the model to the view, also business logic

</small>

---

## Comments on MVC

* **MVC is a _goal_**
    - treat it like other best-practices
    - sometimes real-world requirements blur the boundaries
* Not everyone will agree
* Focus on separation of _presentation_ from _functionality_.

>  The best rubric ever: "We need SMART Models, THIN Controllers, and DUMB Views"<br><small>&mdash; http://c2.com/cgi/wiki?ModelViewController</small>

---

## Real-World Moving Parts

* Client Requests  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"> &nbsp; </div>
* Router  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"> &nbsp; </div>
* Objects  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"> &nbsp; </div>
* Presentation Layer  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"> &nbsp; </div>
* Business Logic  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"> &nbsp; </div>
* Persistence  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"> &nbsp; </div>

<!-- .slide: data-transition="fade" -->

+++

<!-- .slide: data-transition="fade" -->

## Real-World Moving Parts

* Client Requests  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"><b>controller</b></div>
* Router  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"><b>controller</b></div>
* Objects  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"><b>model, view, controller</b></div>
* Presentation Layer  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"><b>view</b></div>
* Business Logic  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"><b>controller</b></div>
* Persistence  <div style="float: right; width: 13em; text-align: left; padding-left: 1.2em;"><span style="font-size:75%;"><b>model? controller?</b>&nbsp;(data-mapper)</span></div>

---

## Client Requests

Client requests are actually handled outside of the _business logic_ of your application.  They take place between the client (software) and server (software).

* HTTP Requests
* `GET`, `POST` are most common, simplest
* _Path_ part of URL selects functionality
* URL Rewriting

---

## Router

The application's _router_ is responsible for dispatching requests according to the path portion of the URL.

* Traditional Routing
    - uses directory/file structure
    - works best for "static" sites
* URL Rewriting
    - Requires support from server
    - allows "cleaner" user-facing URLs

<small>http://httpd.apache.org/docs/2.0/misc/rewriteguide.html<br>http://httpd.apache.org/docs/current/rewrite/</small>

---

## (Application) Objects

We will will (ab)use the term _Application Object_ to refer to all entities for which our application must maintain state data.  <i>(Don't confuse this with actual instances of a `class` within the application code.)</i>

**Examples**
<small style="font-size: 100%; display: block; margin-left: .5em; width: 800px; text-align: left;">

* Blog Post
* Comment
* User

</small>

---

## View (Presentation) Layer

The View layer code generation may be split across the client-side and server-side, although final display and interaction is a client-side responsibility.

* Server-side templates
    - Raw PHP templates
    - Handlebars, Twig, Smarty, Plates, etc.
* Client-side dynamic elements
    - Raw JavaScript
    - React.js, AngularJS, JQuery, etc.

---

## Control Layer

Control may also "live" on both the client- and server-side.  All "trusted" control logic (business logic) must be on the server-side.

* Controllers ideally provide mapping between _view_ and _model_.
* Incidental functionality also falls into the controller category.
    - routing
    - access control
    - caching

---

## Persistence

The data from the _model_ layer must be stored (_persisted_) for later use.  The model should not be directly aware of _how_ this happens.

* _Data-Mapper_ - provides a layer of abstraction between the persistence mechanism and the Model Object.
* A data-mapper is sometimes considered part of the _model_, or sometimes part of the _controller_.
    - The truth is that it is really a separate layer.

---

<!-- .slide: data-background="assets/images/grumpy-cloud-outline.jpg" class="bg-box" -->

## MVCRD?

_Model-View-Controller-Router-DataMapper?_

* **Keep It Simple!**
    - Remember the _separation of concerns_
        + Keep _business logic_ away from _presentation_
        + Keep _models_ as _storage-agnostic_ as possible
    - Don't sweat the details of "Pure MVC"
        + When in doubt, see top bullet point.

---

<!-- .slide: data-background="assets/images/cloud_sparks.jpg" class="bg-box" -->

## Too Many Terms/Buzzwords?

That's OK.  

Work on memorizing terms, but we will _learn by building_.  The moving parts will make more sense when you see them work (one piece at a time).

Let's get building!

---

## Resources

http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller

http://c2.com/cgi/wiki?ModelViewController

http://httpd.apache.org/docs/2.0/misc/rewriteguide.html

http://httpd.apache.org/docs/current/rewrite/

http://en.wikipedia.org/wiki/Observer_pattern

http://stackoverflow.com/questions/13829231/php-mvc-user-authentication-and-global-user-object


