
## Supplemental Material:
# JavaScript Objects

---

## "Traditional" Prototype-based Objects

---

Traditionally, objects are created by calling a _constructor function_.  Constructor functions look like this:

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
```

Note the use of the `this` keyword to create _instance_ members (attributes and methods).  

---

You can also create "_object-local_" members:

```javascript
function Guess(){
    let secret = -1;
    this.check = function(x) {
        return x == secret;
    }
    this.reset = function() {
        secret = Math.floor(Math.random() * 5);
    }
    this.reset();
}
```

These simulate "private" attributes.

---

## Instance Methods

A method may be created just by assigning an anonymous function to an object attribute in a constructor function:

```javascript
function Homework(title, ptsPossible, ptsEarned){
    this.title       = title;
    this.ptsPossible = ptsPossible;
    this.ptsEarned   = ptsEarned || 0;        // default: 0
    this.percent     = function(){            // instance method
        return this.ptsEarned / this.ptsPossible; 
    };
}
```

In this case, the function becomes an _instance member_ of each object the constructor creates.

* Each instance has its own copy of the function
    - This could waste memory

---

## Prototype Methods

You may also inject a method into the _prototype_ for an object:

```javascript
function Homework(title, ptsPossible, ptsEarned){
    this.title       = title;
    this.ptsPossible = ptsPossible;
    this.ptsEarned   = ptsEarned || 0;        // default: 0
}
Homework.prototype.percent = function(){      // add to prototype
    return this.ptsEarned / this.ptsPossible; 
};
```
<small style="font-size: 85%;" >
In this case, the function is _shared_ by all instances of `Homework`.

* less memory use  (good)
* faster construction (good)
* slightly slower method call (bad)
* no access to object-local variables (maybe OK, maybe bad)

</small>

---

```javascript
function Guess(){
    let secret = -1;
    
    this.reset = function() {
        secret = Math.floor(Math.random() * 5);
    }
    this.reset();
}

Guess.prototype.check = function(x) { 
    return x == secret;  // FAILS! `secret` is object-local!
}
```

This **won't work** --- the `check()` method cannot access the object-local attribute `secret`:

```bash
> a = new Guess();
> a.check(3);
ReferenceError: secret is not defined
    at Guess.prototype.check:11:5
    at eval:1:1
```

---

<!-- .slide: data-background="assets/images/question_cloud2.jpg" class="bg-box" -->

## Which way is Correct?

_It depends..._

* Prototype methods are probably "best practice" in most cases
    - saves memory in the app (especially for large numbers of objects)
    - slightly slower calls are probably not a problem
* Instance methods are "better" when:
    - fast calls are a necessity
    - method must access "private" (constructor-local) variables

---

## "Modern" ES6 Classes

---

In ES6-compatible environments, you can define classes that look more like other OO-languages:

```javascript
class Car {
    constructor(make, model, year, drive_action=null){
        this.make  = make;
        this.model = model;
        this.year  = year;
        if(drive_action !== null){
            this.drive = drive_action;
        }
    }
    drive() {
      console.log("Vroom Vroom");
    }
}

```

---

There is no direct way to have "private" members in the ES6 style.

```javascript
class Guess {
    constructor(){
        let secret = -1;
        this.reset();
    }
    reset(){
        secret = Math.floor(Math.random() * 5);  // OOPS! creates a global!
    }
    check(x){
        return x == secret;
    }
}
```

<small style="font-size: 80%;">
The `let secret = -1;` scopes `secret` to the _constructor_ only ... the use of `secret` in `reset()` actually **creates a global** named `secret`... Which is sort of the opposite of "private"!
</small>

```bash
> a = new Guess();
> secret
4
```

---

<small style="font-size: 90%; min-width: 100%;">
Long way around:  You can have privacy in ES6, but it is ugly...

```
class Guess {
  constructor(){
      let secret = -1;
      
      Object.assign(this, {
          reset() {
              secret = Math.floor(Math.random() * 5);
          },
          check(x) {
              return x == secret;
          }
      });
      
      this.reset();
  }
}
```

```bash
> a = new Guess();
> a.check(3);
true   
> secret
ReferenceError: secret is not defined
    at eval:1:1   a.secret
> Reflect.ownKeys(a)
[ 'reset', 'check' ]
```

<small><a href="http://www.2ality.com/2016/01/private-data-classes.html">http://www.2ality.com/2016/01/private-data-classes.html</a></small>

</small>

---

Resources

http://thecodeship.com/web-development/methods-within-constructor-vs-prototype-in-javascript/

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript

http://www.w3schools.com/js/js_object_definition.asp

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/class

http://javascriptplayground.com/blog/2014/07/introduction-to-es6-classes-tutorial/

http://www.2ality.com/2016/01/private-data-classes.html


