## Supplemental Material:
# PHP Namespaces and Class Autoloading

---

## Namespaces

PHP Namespaces, like those in C++, are used to prevent name collisions in large applications.

* A script can be placed in a namespace by using the `namespace` directive
    - Must be the _first executable statement_ in the file.
* Namespaced identifiers are specified using `\` (the backslash) as the scope-resolution operator:
    - `App\Controllers\MyController`
        + `MyController` is the `class`, in the `Controllers` NS, in the `App` NS.

---

## Autoloading Classes

PHP is capable of _autoloading_ classes.  This means that when you try to instantiate a class that isn't defined yet, the interpreter will look up its definition.

* Must provide an _autoload_ function.
    - `spl_autoload_register()` is used to register 
* May have many _autoload_ functions, or just one.

<small>http://www.sitepoint.com/autoloading-and-the-psr-0-standard/</small>

---

## Example

Consider the following directory structure, where Models, Views, and Controllers each have a directory below the main application directory, and a script defining the autoloading rules in `include/autoload.php`:

```asciidoc
app/
    Controllers/
        Object1.php
        Object2.php
    Models/
        Object1.php
        Object2.php
    Views/
        Object1.php
        Object2.php
    include/
        autoload.php    
    public/
```

---

<style>
pre { min-width: 800px;}
</style>

## Example (continued)

The file `include/autoload.php` might look like this:<small style="font-size: 85%;">

```php
<?php
/**
 * @file    autoload.php
 * @details This file sets up a generic autoloader for classes in which
 *          the class name matches the directory name, with namespace 
 *          names determining the directory hierarchy.
 */

/**
 * loads the file associated with a class name, 
 * by turning the namespace parts into directory 
 * structure.
 * @param $className string  the name of the class to load
 */
function autoloadClassFromDirectory($className){
    // switch namespace format to directory format:
    $class_name = str_replace('\\', DIRECTORY_SEPARATOR, $className);   
    require __DIR__ . '/../' . $className .  '.php';
}
// Now register the autoloader:
spl_autoload_register("autoloadClassFromDirectory");
```
</small>

---

<!-- .slide: data-background="assets/images/cloud_sparks.jpg" class="bg-box" -->

## Resources

http://php.net/manual/en/language.namespaces.php

http://www.sitepoint.com/autoloading-and-the-psr-0-standard/



