# The Document Object Model

---

<!-- .slide: data-background="images/cloud-speech-bubble.svg" -->

## Content <=> Object

Quoth the Wikipedia:
<blockquote style="font-size: 80%;">
    The _Document Object Model_ (DOM) is a cross-platform and language-independent convention for representing and interacting with _objects_ in HTML, XHTML, and XML documents.  The nodes of every document are organized in a tree structure, called the _DOM tree_. Objects in the DOM tree may be addressed and manipulated by using _methods_ on the objects. The public interface of a DOM is specified in its _application programming interface_ (API).
</blockquote>


<small>http://en.wikipedia.org/wiki/Document_Object_Model</small>

---

### New Terms

* **objects**
    - "Things" you can represent and interact with in a programming language. <small>(Like variables, but with more capability.)</small>
* **tree structure**
    - hierarchical structure where a _parent_ object may have many _child_ objects, and so on.  
* **methods**
    - functions that are "owned by" or "attached to" an object
* **API**
    - Application Programming Interface - a published specification for how to interact with an application or library.

---

## Visualize the DOM

Consider the following HTML:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello.</title>
    </head>
    <body>
        <h1>Example</h1>
        <p>
            Hello, there.
            Click <a href="http://google.com">here!</a>
        </p>
        <p>
            This is more text.
        </p>
    </body>
</html>
```

----

#####The HTML from the previous slide would result in this DOM representation:

![DOM](images/DocumentObjectModel1.svg "Document Object Model")<!-- .element: style="height: 570px;" class="center" -->

---

### Where is the Content?

![DOM](images/DocumentObjectModel1.svg "Document Object Model")<!-- .element: style="height: 370px;" class="center" -->

See all of those ovals?  That is the _text_ inside the element.     
`textContent`      
You can also access the full HTML content.     
`innerHTML`

---

<!-- .slide: data-background="images/white_cloud.jpg" -->

## Tools

* **Firefox**
    - Built-in Developer Tools
    - DOM Inspector
* **Chrome**
    - Built in Developer Tools

---

## Identifying Elements

How do you identify a particular element that you want to observe or modify?

* **`id`** attributes allow _unique naming_ of elements within the DOM.
* Once an element has an `id`, you can find it by using the `document`'s `getElementById()` method.
* It is also possible to select elements by `name`, `class`, or by `tag`, but the results are arrays, not individual objects.


---

## Links

http://en.wikipedia.org/wiki/Document_Object_Model

https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent

https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML

http://perfectionkills.com/the-poor-misunderstood-innerText/
