# HTML

<img src="images/HTML5_logo.png" class="center" style="margin: 0 auto; max-height: 350px;" />

---

## 10<sup>*</sup> Essential Tags

<small style="font-size: 88%;"><sup>*</sup>For some definition of the number 10...

1. `<h1> - <h6>`   Heading
2. `<p>` Paragraph
3. `<i>` Italic & `<em>` Emphasis
4. `<b>` Bold & `<strong>` Strong
5. `<a>` Anchor
6. `<ul>` & `<li>`   Unordered List & List Item
7. `<blockquote>`  Quotation
8. `<hr>`  Horizontal Rule
9. `<img>` Image
10. `<div>` Division & `<span>` Span

</small>


---

## `<h1> - <h6>` Heading

Creates larger text designed to represent a "Heading".

```html
<h1>Main Heading</h1>
<p>Hello.  This is a paragraph.</p>
<h2>Secondary Heading</h2>
<p>This is another paragraph.</p>
```
Renders as:

<iframe style="min-height: 220px;" srcdoc='
    <h1>Main Heading</h1>
    <p>Hello.  This is a paragraph.</p>
    <h2>Secondary Heading</h2>
    <p>This is another paragraph.</p>
'></iframe>

---

## `<p>` Paragraph

Denotes a paragraph of text.

```html
<p>Hello.  This is a paragraph. Lorem ipsum dolor sit amet, 
consectetuer adipiscing elit.</p>
<p>This is another paragraph. Aenean commodo ligula eget 
dolor. Aenean massa. Cum sociis natoque penatibus et magnis 
dis parturient montes, nascetur ridiculus mus.</p>
```

Renders as:

<iframe  srcdoc='
    <p>Hello.  This is a paragraph. Lorem ipsum dolor sit amet, consectetuer
    adipiscing elit.</p>
    <p>This is another paragraph. Aenean commodo ligula eget dolor. Aenean massa.
    Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.</p>
'></iframe>

---

## `<i>` Italic & `<em>` Emphasis

Used to denote text that should be _italicized_.
If the text should be _emphasized_, use `<em>`; otherwise, use `<i>`.

```html
<p>This is an <em>important thing</em> to remember.</p>
<p>The book was named <i>War and Peace</i>.</p>
```

Renders as:

<iframe  srcdoc='
    <p>This is an <em>important thing</em> to remember.</p>
    <p>The book was named <i>War and Peace</i>.</p>
'></iframe>

<span style="font-size: 80%;">
http://engineeredweb.com/blog/2013/html5-semantic-diff-bold-strong/
</span>

---

## `<b>` Bold & `<strong>` Strong

Used to denote text that should be **bold**.
If the text is bold to indicate **importance**, use `<strong>`; otherwise, use `<b>`.

```html
<strong>Digitigradient</strong>: 
    <b>verb</b> &mdash; To walk on your toes like a dog or cat. 
```

Renders as:

<iframe  srcdoc='
   <strong>Digitigradient</strong>: 
    <b>verb</b> &mdash; To walk on your toes like a dog or cat. 
'></iframe>

<span style="font-size: 80%;">
http://engineeredweb.com/blog/2013/html5-semantic-diff-bold-strong/
</span>

---

## `<a>` Anchor

The _anchor_ tag has has two purposes:

1. to create a hyperlink (an outgoing link)
    * this is the most common use
2. to create an _anchor_ (for incoming links)
    * this is where the name of the tag comes from

---

### `<a>` Examples

```html
<h4>Outgoing Link</h4>
<p>Click <a href="http://google.com">here</a> to visit
the Google website.</p>
<h4>Anchor (target)</h4>
<p><a name="example" rel="internal">This</a> paragraph 
is anchored.</p>
<p>Click <a href="#example">here</a> to go to the previous 
paragraph.</p>
```

Renders as:

<iframe  style="min-height: 220px;" srcdoc='
    <h4>Outgoing Link</h4>
    <p>Click <a href="http://google.com">here</a> to visit
    the Google website.</p>
    <h4>Anchor (target)</h4>
    <p><a name="example" rel="internal">This</a> paragraph 
    is anchored.</p>
    <p>Click <a href="#example">here</a> to go to the previous 
    paragraph.</p>
'></iframe>

---

## `<ul>` & `<li>`  List & Item

Creates an <em>**u**nordered **l**ist</em> (bulleted-list) & <em>**l**ist **i**tems</em>.

```html
<ul>
    <li>This is a list item.</li>
    <li>This is a second one.</li>
    <ul>
        <li>Lists can be nested too.</li>
    </ul>
</ul>
```

Renders as:

<iframe srcdoc='
    <ul>
    <li>This is a list item.</li>
    <li>This is a second one.</li>
        <ul>
            <li>Lists can be nested too.</li>
        </ul>
    </ul>
'></iframe>

_Change `<ul>` to `<ol>` for a **numbered** (**o**rdered) **l**ist._

---

## `<blockquote>`  Quotation

Marks a section of text as a direct quote.

```html
<blockquote cite="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote#Summary">
    <p>The HTML <tt>blockquote</tt> Element (or HTML Block Quotation 
    Element) indicates that the enclosed text is an extended 
    quotation. Usually, this is rendered visually by indentation 
    (see Notes for how to change it). A URL for the source of 
    the quotation may be given using the <tt>cite</tt> attribute, 
    while a text representation of the source can be given using 
    the <tt>cite</tt> element.</p>
</blockquote>
```

Renders as:

<iframe srcdoc='
    <blockquote cite="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote#Summary">
        <p>The HTML <tt>blockquote</tt> Element (or HTML Block Quotation Element) indicates that the enclosed text is an extended quotation. Usually, this is rendered visually by indentation (see Notes for how to change it). A URL for the source of the quotation may be given using the <tt>cite</tt> attribute, while a text representation of the source can be given using the <tt>cite</tt> element.</p>
    </blockquote>
'></iframe>


---

## `<hr>`  Horizontal Rule

Places a horizontal line across the page --- used to separate large sections visually.

```html
<p>This is one section.</p>
<hr>
<p>And this is another</p>
```

Renders as:

<iframe srcdoc='
    <p>This is one section.</p>
    <hr>
    <p>And this is another</p>
'></iframe>

---

## `<img>` Image

Inserts an image into the page.  The `src` attribute tells the path to the image, which may be local or a URL.

```html
<p><img src="images/i-tag-cat-small.jpg"> Italicat says "Hi".</p>
```

Renders as:

<iframe style="min-height: 230px;" srcdoc='
    <p>
       <img src="images/i-tag-cat-small.jpg"> 
       Italicat says "Hi".
    </p>
'></iframe>

---

## `<div>` Division & `<span>` Span

`<div>` creates a _block-level_ division in a page.    
`<span>` allows styling small items inline.

<small style="float:left; width: 3em; font-weight: bolder;">HTML:</small>
```html
<div>This is a block of text.</div>
<div>This is another block of text.</div>
<p>You can use a <span>span</span> to style inline items.</p>
```
<small style="float:left; width: 3em; font-weight: bolder;">CSS:</small>
```css
/* CSS: */
div  { border: 1px dotted cornflowerblue; }
span { border: 1px dashed red;            }
```

Renders as:

<iframe srcdoc='
    <style>
        div  { border: 1px dotted cornflowerblue; }
        span { border: 1px dashed red;            }
    </style>
    <div>This is a block of text.</div>
    <div>This is another block of text.</div>
    <p>You can use a <span>span</span> to style inline items.</p>
'></iframe>

---

## Was that 10?

&nbsp;<br>&nbsp;<br>&nbsp;<br>&nbsp;<br>

<!-- .slide: data-background="images/business_cloud.jpeg" -->


---

## New HTML5 Tags

HTML5 adds several new _semantic elements_.  The following 7 are worth memorizing:

![semantic layout](images/semantic_elements.gif "Semantic elements example layout")<!-- .element: style="float: right; height: 280px;" -->

* `<header>`
* `<nav>`
* `<section>`
* `<article>`
* `<aside>`
* `<footer>`

---

#### Bigger list of Semantic Elements
<table class="center" style="font-size: 45%; cellpadding: 3px; cellspacing: 3px;">
<tr><th style="width:20%">Tag</th><th>Description</th></tr>
<tr><td>`<article>`</td><td>individual article content</td></tr>
<tr><td>`<aside>`</td><td>content aside from the page content</td></tr>
<tr><td>`<details>`</td><td>additional details that the user can view or hide</td></tr>
<tr><td>`<figcaption>`</td><td>caption for a &lt;figure&gt; element</td></tr>
<tr><td>`<figure>`</td><td>self-contained content, like illustrations, diagrams, photos, code 
listings, etc.</td></tr>
<tr><td>`<footer>`</td><td>footer for a document or section</td></tr>
<tr><td>`<header>`</td><td>Specifies a header for a document or section</td></tr>
<tr><td>`<main>`</td><td>the main content of a document</td></tr>
<tr><td>`<mark>`</td><td>marked/highlighted text</td></tr>
<tr><td>`<nav>`</td><td>navigation links</td></tr>
<tr><td>`<section>`</td><td>logical section in a document</td></tr>
<tr><td>`<summary>`</td><td>visible heading for a &lt;details&gt; element</td></tr>
<tr><td>`<time>`</td><td>date/time</td></tr>
</table>
<small>http://www.w3schools.com/html/html5_semantic_elements.asp</small>

---

## HTML Template Tag

HTML5 also added the ability to create "templates" right in your document.

* `<template>` - creates _inert_, clonable DOM elements.
* Will not render until you clone and render it via JavaScript.

<small>http://www.html5rocks.com/en/tutorials/webcomponents/template/</small>

<small>https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template</small>

<!-- .slide: data-background="images/cloud-template.jpg" -->
