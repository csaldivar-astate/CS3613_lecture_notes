
<!-- .slide: data-background="assets/images/js-cover.jpg" -->

## Simple JavaScript

---

## JavaScript

Also known as **ECMAScript**, JavaScript:

* is **not Java** (nor related in any way)
* has a "C-like" syntax
* uses dynamic typing
    - variable type is only determined by the _value_ stored in it at that time.
* supports _anonymous_ (or _lambda_) functions
* is multi-paradigm
    - imperitive / structured
    - object-oriented
    - functional

---

## Syntax

* C-like:
    - statements end with semicolons (although optional in places)
    - array notation preserved (index from zero)
    - Except:   
        + Don't declare your variables with a type!
        + Declaration used `let`
        + Uninitialized values are `undefined`

```javascript
let x;
let y;
x = 4;
if(y === undefined){
    y = 3;
}
let z = y / x;  // Floating-Point division!
```

----

## Operators

Was that a "triple-equal"???  Yes.

Most operators are the same as in C++.  The ones with differences that are worth noting are shown below:

```
Operator | Desc
-----------------------------------------------
 ==     | Equal to (in terms of value)
 ===    | Same as (equal value AND type)
 !=     | Not equal to (in terms of value)
 !==    | Not same as (different value OR type)
 /      | Division (floating-point)
```

How do you do integer division?

```javascript
let quotient  = Math.floor(y / x);
let remainder = y % x;
```

<small style="font-size: 72%;">The `Math` standard library is similar to C++ `<cmath>`, but object-oriented (you use the library name as a prefix).</small>

---

## Dynamic Typing

Dynamic typing is **freedom**!  (to make mistakes)...

```javascript
let x = 12;
let y = x + 2;
x = "Hello ";
let m = x + "World!";
// Now y contains 14 and m contains "Hello World!"
```
Notice that `+` _concatenates_ strings.    
Also, you can use either single- or double-quotes for strings:

```javascript
let msg  = "This string is double-quoted.";
let msg2 = 'But single quotes work as well.';
let msg3 = '"Oh, my," he said.';
```

---

## Lambdas

You may need to use a function _once_, but there is no need to name it.  This is a _lambda_ function.

* useful for storing a function in a variable
    - _you can store a function in a variable in JavaScript_
* useful for passing a function as an argument to another function

```javascript
let tau = function(){ return 2 * Math.PI; };
let x   = tau();
```

---

## Imperitive

```javascript
function foo( x, y ){
    return 3 * x + y / 2;
}

function bar( x ){
    let a = foo(x, x);
    a += foo(a, x);
    return a;
}

function baz( x ){
    for(let i = 0; i < bar(x); i++){
        console.log(bar(i));
    }
}
```

---

## Object-Oriented

```javascript
// Object constructor function
function Car(make, model, year, drive_action){
    this.make  = make;
    this.model = model;
    this.year  = year;
    this.drive = drive_action || function(){ 
                    console.log("Vroom Vroom"); 
                 }
}

let mycar = new Car("Toyota", "Prius", "2015"); // create a car

let truck = new Car("Toyota", "Tacoma", "2007", function(){
    console.log("RrrRrrRrr RrrRrrRrr");         // Mud tires? 
});

mycar.drive();  // prints "Vroom Vroom" to log
truck.drive();  // prints RrrRrrRrr RrrRrrRrr" to log 
```

---

## JSON-Style Objects

```javascript
// Object-Initializer Notation
// AKA "JSON"
let mycar {
    make:  "Toyota",
    model: "Prius",
    year:  2015,
    drive: function(){ console.log("Vroom Vroom"); }
};

mycar.drive(); // Vroom Vroom
```

**Advantage**: Great for moving data around.     
**Disadvantage**: No enforced interface.

---

## Functional

```javascript
function forEach(list, action) {
    for (let i = 0; i < list.length; i++) {
        action(list[i]);
    }
}
function map(mappingFunction, list) {
    let result = [];
    forEach(list, function (item) {
        result.push(mappingFunction(item));
    });
    return result;
}
function doubleIt(item) {
    if (typeof item === "number") {
        return item * 2;
    }
    else if(typeof item === "string") {
        return item + item;
    }
}
console.log(map(doubleIt, [1, 2, 3, 4, 5, "Woot"]));
```

<small>http://www.srirangan.net/2011-12-functional-programming-in-javascript</small>

---

## Interact with the DOM

The easiest way to interact with elements of the DOM is to give them a unique `id` attribute.  Then, use the `document.getElementById()` method to "look up" the element you want to interact with.

Different elements will expose slightly different attributes/methods &mdash; references are plentiful online.

```javascript
function flashMessage( msg ){
    // query to "select" the "flash-box" element in the DOM:
    let flashbox       = document.getElementById('flash-box');
    flashbox.innerHTML = msg;        // change message in box
    showFlashBox();                  // show the box
    setTimeout(hideFlashBox, 20000); // hide in 20 seconds
}
```

----

```javascript
function showFlashBox(){
    // query to "select" the "flash-box" element in the DOM:
    let flashbox = document.getElementById('flash-box');
    // setting `display` to "block" will make the element
    // visible, and make it behave as a "block element"
    flashbox.style.display = "block";
}
function hideFlashBox(){
    // query to "select" the "flash-box" element in the DOM:
    let flashbox = document.getElementById('flash-box');
    // Setting `display` to "none" will remove the element from 
    // the visible page.
    flashbox.style.display = "none";
}
function flashMessage( msg ){
    // query to "select" the "flash-box" element in the DOM:
    let flashbox       = document.getElementById('flash-box');
    flashbox.innerHTML = msg;        // change message in box
    showFlashBox();                  // show the box
    setTimeout(hideFlashBox, 20000); // hide in 20 seconds
}
```

---

## Events

Many DOM elements can respond to events (usually initiated by user interaction with the GUI).  Examples:

* `onclick` - user clicked on the element
* `dblclick` - user double-clicked on the elements
* `onload` - a frame or document is loaded
* `onkeypress` - when a keyboard key is pressed
* `onsubmit` - when a form is submitted

See <small>http://en.wikipedia.org/wiki/DOM_events#Common.2FW3C_events</small>

---

## Arrays

Work more or less like C++ arrays, except _dynamic_!

```javascript
let fruit = ['apple', 'banana', 'canteloupe', 'durian'];

for(let i = 0; i < fruit.length; i++){
    console.log(fruit[i]);
}
```

JavaScript arrays know their own <tt>length</tt>!


**Information**
<small>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array <br>
http://www.w3schools.com/jsref/jsref_obj_array.asp
</small>

---

## Arrays

Other nifty JS Array tricks:

```javascript
let fruit = ['apple', 'banana', 'canteloupe', 'durian'];
// loop in a functional style:
fruit.forEach( function(x){ console.log(x); } );
// Reverse:
fruit = fruit.reverse();
// Sort:
fruit = fruit.sort();
// Add/remove at back
fruit.push('elderberry');
console.log(fruit.pop());   // elderberry (removed and returned)
// Or front:
console.log(fruit.shift()); // apple (removed and returned)
fruit.unshift('apple');     // puts apple back at front
// Join (into string)
let str = fruit.join(", "); // makes comma-space separated string
console.log(str);
```

---

## Local Storage

You can store data on the client-side either temporarily (_sessionStorage_) or "permanently" (_localStorage_).

* Storage is per-_origin_ (domain+protocol).
* All pages from the same origin share the storage.
* You can use this for _persistence_ or for _communication_ among tabs.
* There are also local databases, and filesystems, but these are less supported.

**More Information:**

https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API

---

## Resources

**Practice**

http://repl.it

https://jsfiddle.net/

**Reference**

<article style="font-size: 55%; text-align: left;">
https://developer.mozilla.org/en-US/docs/Web/JavaScript<br>
http://en.wikipedia.org/wiki/DOM_events#Common.2FW3C_events<br>
http://www.srirangan.net/2011-12-functional-programming-in-javascript<br>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array <br>
http://www.w3schools.com/jsref/jsref_obj_array.asp<br>
https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API
</article>