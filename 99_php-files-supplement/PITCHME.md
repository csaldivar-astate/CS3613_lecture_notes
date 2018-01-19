## Supplemental Material:
# File I/O in PHP

<!-- .slide: data-background="assets/images/cloudfilestorage.jpg" class="bg-box" -->

---

## Open / Use / Close

Basic file operations in PHP closely resemble those in other languages.  One difference from C++ is that PHP file manipulation is exposed via _functions_, not _objects_.

* `fopen()` - open
* `fread()`, `fseek()`, `fwrite()`, etc. - file I/O operations
* `fclose()` - close

<small>http://php.net/manual/en/ref.filesystem.php</small>

---

## Open

The `fopen()` function opens a file and returns a resource "handle" that represents the file.

**Syntax**<br>
&nbsp;&nbsp;&nbsp;&nbsp; `fopen( `_`$filename`_`,`_`$mode`_`)`

* `fopen()` returns a _file resource_. (AKA "file handle")
* Common modes:
    - `r`, `r+` - read, read/write (no create)
    - `w`, `w+` - write, read/write (create)
    - `a`, `a+` - append, read/append (create)
    - `b` - _binary_ mode (always recommended)

---

## I/O Operations

* `fflush( `_`$file_resouce`_` )` — Flushes the output to a file
* `fgets( `_`$file_resource [`_`,`_` $length]`_` )` — Gets line from file pointer
* `fread( `_`$file_resource`_`,`_` $length`_` )` — Binary-safe file read
* `fwrite( `_`$file_resource`_`,`_` $string [`_`,`_` $length]`_` )` — Binary-safe file write
* `filesize( `_`$filename`_` )` - Gets size of file (in bytes)

---

## Close

The `fclose()` function is used to release the system resource when you are finished using it. Closing the file also flushes buffers.

**Syntax**     
&nbsp;&nbsp;&nbsp;&nbsp;`fclose(`_`$file_resource`_`)`

---

### Example 1: Save Session

It is generally a bad idea to put arbitrary amounts of data into the PHP-native _session_.  A better idea would be to store a regular file with the session data in serialized form, then only place that file's name in the PHP-session:

```php
// Assume that `$sessData` is a data structure containing whatever
// information you need to persist for the user...

$sessDataFileName = uniqid($appBasePath);

$sessDataFile     = fopen($sessDataFileName, 'wb');
fwrite($sessDataFile, serialize($sessData));
fclose($sessDataFile);

$_SESSION['sessDataFileName'] = $sessDataFileName;
```

<small>http://php.net/manual/en/function.serialize.php</small>

---

### Example 2: Load Session

Now, you can load the session data back into `$sessData` by reversing the steps:

```php
$sessDataFileName = $_SESSION['sessDataFileName'];
$sessDataFile     = fopen($sessDataFileName, 'rb');
$sessData         = unserialize(
                        fread($sessDataFile, 
                              filesize($sessDataFileName)
                        )
                    );
fclose($sessDataFile);

// Now `$sessData` has whatever data you stored there in its
// native PHP format.
```
<small>http://php.net/manual/en/function.unserialize.php</small>

---

## Resources

http://php.net/manual/en/ref.filesystem.php

http://php.net/manual/en/function.serialize.php

http://php.net/manual/en/function.unserialize.php


