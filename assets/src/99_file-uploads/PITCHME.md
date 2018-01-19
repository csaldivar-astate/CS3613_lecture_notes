# Managing File Uploads
## Supplement

---

## Client-Side

You need a form on the client side that contains a `file` input element:

```html5
<form action="upload.php" method="post" enctype="multipart/form-data">
    <label for="fileToUpload">Select image to upload:</label>
    <input type="file" name="fileToUpload" id="fileToUpload" accept="image/*">
    <input type="submit" value="Upload Image" name="submit">
</form>
```

<small>http://www.w3schools.com/php/php_file_upload.asp<br>
http://www.w3schools.com/tags/att_input_accept.asp</small>

---

## Server-Side

On the server you will need to perform the following:

* Create a directory to store the file (may be done in advance)
* Create a name for the file
* Verify the file contents
* Move the uploaded file into its long-term destination
* Save the file's information into your database (or similar)

---

### Server-Side (bad) Example<small style="font-size: 80%; min-width: 28em; margin-top: -2em;">
```php
$uploadPath    = "uploads/";
$origName      = basename($_FILES["fileToUpload"]["name"]);
$localPath     = $uploadPath . $origName;
$uploadOk      = false;
// Check if image file is a actual image or fake image
if(isset($_POST["submit"])) {
    $check = getimagesize($_FILES["fileToUpload"]["tmp_name"]);
    if($check !== false) {
        echo "File is an image - " . $check["mime"] . ".";
        $uploadOk = true;
    } else {
        echo "File is not an image.";
    }
}
// if everything is ok, try to upload file
if ($uploadOk) {
    if (move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], 
        $localPath)) {
            echo "The file " . $origName . " has been uploaded.";
    } else {
        echo "Sorry, there was an error uploading your file.";
    }

    // TODO NOW: Save the information ($origName) in your Model
}
```
The problem here is that only one file with the same name can safely be saved; this doesn't scale to large numbers of users.
</small><small>http://www.w3schools.com/php/php_file_upload.asp</small>

---

## Dealing with Collisions<small style="font-size: 90%;">

* When two or more files may have the same name, you will have _collisions_.
    - The newer file will overwrite the older one.
    - This should probably be avoided.
* Avoid collisions by creating unique paths for storing files.
    - Many ways:  unique directories, unique filenames, or a combination
* **Recommendation:** In many cases, storing files by hashing them and using the hash as the filename is useful.
    - (almost) no collisions (based on prob. of hash collision)
    - data **de-duplication** is automatic and _free_
</small>
<small>https://en.wikipedia.org/wiki/Data_deduplication</small>

---

## Using Hashes for Filenames<small style="font-size: 85%;">

In this scheme, all files (or maybe just all per-user files) are kept in the same directory.

* When a file is uploaded, hash its contents; the hash becomes the local filename
    - See if that file already exists in the destination directory
        + If so, skip to next step
        + If not, verify file and move file into permanent location
* Store the file's original name along with its hash in the database
* When retrieving the file, use the original name to populate meta-data (headers) when sending to the user; the local (hash) name need not appear
* Use database queries to match files to local versions
    - Delete local version only when the last database reference is removed

</small>

---

### Visual Example

Consider the following images, perhaps both named _`cat.jpg`_:

<div class="center">![cat.jpg](assets/images/cat.jpg "cat.jpg") &nbsp;&nbsp;&nbsp;&nbsp; ![cat.jpg](assets/images/cat-2.jpg "cat.jpg")</div>

----

### Visual Example

Hash the contents of both files to produce unique filenames:

<div class="center">
![cat.jpg](assets/images/cat.jpg "cat.jpg")
<small style="display: block; float:right;">`36694dbdc36c5a74b5423ca08d83aeb1fe0bd3f2`</small>
</div><div class="center">
![cat.jpg](assets/images/cat-2.jpg "cat.jpg")
<small style="display: block; float:right;">`18837556ba37335798b361ec5d6223b36b20d6cd`</small>
</div>

----

### Visual Example

Now, even if _many_ users upload the same image of the sleeping cat:

</div><div class="center">
![Four cat.jpg files](assets/images/four-cat-2s.jpg "Four cat.jpg files.")
<small style="display: block; float:right;">`18837556ba37335798b361ec5d6223b36b20d6cd`<br><br><br>`18837556ba37335798b361ec5d6223b36b20d6cd`<br><br><br>`18837556ba37335798b361ec5d6223b36b20d6cd`<br><br><br>`18837556ba37335798b361ec5d6223b36b20d6cd`<br></small>
</div>

The server will need to store only _one_ copy, at filename `18837556ba37335798b361ec5d6223b36b20d6cd`.

---

### Server-Side (better) Example<small style="font-size: 78%; min-width: 32em; margin-top: -2em;">
```php
$uploadDir     = "uploads/";
$origName      = basename( $_FILES["fileToUpload"]["name"] );
$uploadOk      = false;
// Check if image file is a actual image or fake image
if(isset($_POST["submit"])) {
    $check = getimagesize($_FILES["fileToUpload"]["tmp_name"]);
    if($check !== false) {
        echo "File is an image - " . $check["mime"] . ".";
        $uploadOk = true;
    } else {
        echo "File is not an image.";
    }
}
// if everything is ok, try to upload file
if ($uploadOk) {
    $localName = hash_file('sha512', $_FILES["fileToUpload"]["tmp_name"]);
    $localPath = $uploadDir . $localName;
    // If the file already exists, no need to move it.
    if (!file_exists($localPath)) {
        if (move_uploaded_file($_FILES["fileToUpload"]["tmp_name"],
            $localPath)) {
                echo "The file " . $origName . " has been uploaded.";
        } else {
            echo "Sorry, there was an error uploading your file.";
        }
    }

    // TODO NOW: Save the information ($origName, $localName) in your Model
    
}
```

<small>http://php.net/manual/en/function.hash-file.php</small></small>

---

## Resources

http://www.w3schools.com/php/php_file_upload.asp

http://php.net/manual/en/features.file-upload.php

http://php.net/manual/en/function.hash-file.php

http://php.net/manual/en/features.file-upload.put-method.php

http://php.net/manual/en/function.stream-copy-to-stream.php

http://www.w3schools.com/tags/att_input_accept.asp

https://en.wikipedia.org/wiki/Data_deduplication