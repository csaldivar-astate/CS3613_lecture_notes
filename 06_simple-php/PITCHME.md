
# Simple PHP

<!-- .element: style="height: 400px;" class="center" -->
![PHP Logo](assets/images/PHP-logo.png "PHP Logo")

---

## PHP

Quoth the Wikipedia:
<blockquote style="font-size: 90%;">
PHP is a server-side scripting language created in 1995 and designed for web development but also used as a general-purpose programming language. As of January 2013, PHP was installed on more than 240 million websites (39% of those sampled) and 2.1 million web servers. Originally created by Rasmus Lerdorf in 1994, the reference implementation of PHP (powered by the Zend Engine) is now produced by The PHP Group. While PHP originally stood for _Personal Home Page_, it now stands for _PHP: Hypertext Preprocessor_, which is a recursive backronym.
</blockquote>

<small>http://en.wikipedia.org/wiki/PHP</small>

---

<!-- .slide: style="font-size: 90%;" -->
## PHP

* has a "C-like" syntax
* also has a somewhat Perl-like syntax...
* uses dynamic typing
    - variable type is determined by the value stored in it
    - relatively _weak_ typing (values coerce automatically in many cases)
        + `"5" + 5` is a _valid_ expression, and produces `10`.
* supports _anonymous_ functions (lambdas, or closures)
* is multi-paradigm
    - imperitive / structured
    - object-oriented (more than JavaScript)
    - functional

---

## Syntax<!-- .slide: style="font-size: 90%;" -->

* C-like:
    - statements end with semicolons
    - array notation preserved (but arrays are _associative_)
    - Major Differences:
        + Don't declare variables
        + Variable names must begin with `$`
            * Except global constants/macros
        + Uninitialized values default based on their type.
            * generally "empty"- "zero"- or "FALSE"-_ish_.
        + Boolean literals are `TRUE` and `FALSE`

```php
$x   = 4;
$y   = 3;
$z   = $y / $x; // Floating-Point division!
$y   = "3";     // string containing 3...
$hmm = $y / $x; // also 0.75! Wow.
```

---

## Operators

Notable differences from C++:
```asciidoc
Operator | Desc
-----------------------------------------------
 ==     | Equal to (in terms of value)
 ===    | Same as (equal value AND type)
 !=     | Not equal to (in terms of value)
 !==    | Not same as (different value OR type)
 /      | Division (floating-point-ish)
 .      | String concatenation operator
 \      | Class hierarchy separator (also escape)
```

There are `integer` and `double` types in PHP:
```php
echo gettype(3 / 4); // prints "double"
echo gettype(4 / 2); // prints "integer"
```
<small style="font-size: 75%">Division gives back the _most appropriate type_ (either `integer` or `double`) depending on the operands!</small>

---

## PHP and HTML

PHP was designed to be directly embedded in HTML, so it has HTML-like _open_ and _close_ tags:

```php
<p>There are <?php echo $numberOfLights ?> lights!</p>
```

As a consequence, even pure PHP scripts must begin with the open tag: `<?php `.  Current best-practice: pure-PHP scripts have no close tag.

```php
<?php
// This is a pure PHP script. Nothing should 
// precede the "open" tag above.
function squareValue( $value ){
    return $value * $value;
}
// there should be no "close" tag...  
// This is the end of the file.
```

---

## HTML and PHP

To keep display elements separate from functional code, keep most functionality in a pure-PHP script.  Write most HTML in a _template_ file, including PHP code _sparingly_ to integrate dynamic values:

```html5
<p>Hello, <?= $userName ?>.  Welcome to our site.</p>
<p>You have <?= $unreadMsgCount ?> new messages.</p>
```

Note the _PHP value tag_ (A.K.A. "short echo tag") used above: (`<?= ... ?>`)  The value tag can only contain code that evaluates directly to a value (variables, etc.).  You should not perform complex operations inside the value tag.

---

## `include` and `require`

PHP's analog of the C++ preprocessor `#include` directive are the `include()` and `require()` functions (and variations):

```asciidoc
include( "filename" );      // paste "filename" content here
include_once( "filename" ); // will not multiple-include
require( "filename" );      // kills script if file not found
require_once( "filename" ); // will not multiple-include
```

---

## Strings in PHP

* double-quoted strings: regular variables are evaluated; escape characters work as usual
* single-quoted strings: will _not_ evaluate variables or escape characters
* Heredoc notation: used for multi-line strings (see below)
* Nowdoc notation: multi-line with no variable evaluation

```php
$name = "Bob";
echo "Hello, $name!"; // prints "Hello, Bob!"
echo 'Hello, $name!'; // prints "Hello, $name!"
// HEREDOC:
$example = <<<EOS
Hello, $name!
Welcome back.
Our newest products are shown below:
EOS;
echo $example;        // prints all three lines
```

---

## Objects

PHP Classes look very similar to C++ (or even Java) classes:

```php
class Car{
    public $make;   // you can define attributes,
    public $model;  // (or "properties") with access
    public $year;   // levels public, private, protected.
    // methods also have access levels
    public function __construct($make, $model, $year){
        $this->make  = $make;
        $this->model = $model;
        $this->year  = $year;
    }
    public function drive(){  
        echo "Vroom Vroom";
    }
}

$mycar = new Car("Toyota", "Prius", 2015);
$mycar->drive();
```

----

```php    
    public function __construct($make, $model, $year){
        [...]
    }
```

Notice the double-underscore at the beginning of `__construct()`.  Such an identifier has special meaning in PHP (this one is the _constructor_ for `class Car`). 

Read about PHP _"Magic Methods"_ for more info.

<small>http://php.net/manual/en/language.oop5.magic.php
</small>

---

## Access Levels

PHP Access levels work similarly to C++:

* `public` - allows access from external code
* `protected` - allows access within the class and any derived class
* `private` - restricts access to code contained within the class

---

## Class Auto-Loading

PHP allows `class` definitions to be _auto-loaded_.

* You provide a special function that performs the loading operation (by including a script containing the appropriate `class`).
* When you try to instantiate a new object whose type is (at that moment) _unknown_, the auto-loading function will attempt to load its `class`.
* If setup properly, this reduces the need for `include` or `require` directives.

<small>http://php.net/manual/en/function.spl-autoload-register.php</small>

---

<!-- .slide: data-background="assets/images/grumpy_cloud.gif" class="bg-box" -->

## Bad PHP

PHP was born _before_ the "Web 2.0" "revolution"; back when the `<blink>` tag was still in use.  It is an easy langage to use, but does not _encourage_ best practices.

_You can write beautiful PHP, but you have to **want** to._

Bad example from Wikipedia:
```php
<body>
    <?php echo '<p>Hello World</p>'; ?>
</body>
```

---

<!-- .slide: data-background="assets/images/happy-cloud.png" class="bg-box" -->

## Good PHP

* Stick with general style tips learned from C++.
* **Separate Concerns**
    + Keep functional code out of visual templates (as much as possible) and vice-versa.
* Don't rely on "uninitialized variables default" behavior.
* Separate logic into small script files.
    - Each file should contain related logic about "one thing".
    - i.e. C++ one-`class`-per-header-file philosophy
* Where PHP offers many ways to do a thing, pick one and stick with it.

---

## PHP 7

http://blog.teamtreehouse.com/5-new-features-php-7

https://blog.engineyard.com/2015/what-to-expect-php-7

---

## Resources

http://php.net

http://php.net/manual/en/language.oop5.php

http://php.net/manual/en/language.oop5.magic.php

http://php.net/manual/en/function.spl-autoload-register.php

