## Supplemental Material:
# PHP Templates

---

## Templates

The idea behind a _template_ file is to create something that is close to "pure HTML" as possible, while also incorporating dynamic data.  This can easily be done in "pure" PHP, while maintaining a clean template.

**Templating Features:**

* PHP value tags (AKA "echo" tags)
* Alternative control structure syntax

---

## PHP Value Tags

The `<?=  ...  ?>` tag syntax automatically evaluates the expression contained between the open and close tag, and `echo`s the result into the HTML document.

* Best for variables, but function calls are also OK.
* Avoid placing arbitrary code in the value tags.

```html5
<p>
    Welcome back, <?= $userName ?>. 
    You have <?= $msgCount ?> unread messages.
</p>
```

---

## Alternative Control Structure Syntax

To provide a cleaner alternative to the "curly-brace" enclosed bodies of control structures, PHP provides an alternative syntax that looks cleaner when embedded in HTML.

* Each control structure's block opens with a colon (`:`) instead of an opening curly-brace.
* There is a _closing keyword_ for each control structure instead of the closing curly-brace.

---

### List of Alternative Control Structures

```asciidoc
Open              |  Close Keyword
-----------------------------------
if( ... ):        |  endif;
while( ... ):     |  endwhile;
for( ... ):       |  endfor;
foreach( ... ):   |  endforeach;
switch( ... ):    |  endswitch;
```

---

### Example

```html5
<p>
    <?php if($msgCount > 0): ?>
        You have $msgCount new messages.
    <?php else: ?>
        No messages...  Go enjoy your day!
    <?php endif; ?>
</p>
```

---

### Example

```html5
<p>
    <?php for($i = 0; $i < $msgCount; $i++): ?>
        <div class='message' id='msg-<?= $i + 1 ?>'>
            <?= $messages[$i] ?>
        </div>
    <?php endfor; ?>
</p>
```

---

### Example

```html5
<p>
    <?php foreach($replies as $user => $msg): ?>
        <div class='reply'>
            <span class="byline">Posted by: <?= $user ?></span>
            <span class="msg-body"><?= $msg ?></span>
        </div>
    <?php endforeach; ?>
</p>
```

---

### Example

```html5
<span class='feels-like'>
    <?php if($temperature < 32): ?>
        Freezing
    <?php elseif($temperature < 50): ?>
        Chilly
    <?php elseif($temperature < 80): ?>
        Nice
    <?php else: ?>
        Hot
    <?php endif; ?>
</span>
```

You _must_ use the **`elseif`** keyword when using the alternate syntax; the `else if` sequence will not work.

---

### Can "normal" (curly-brace) syntax be used?

_Yes,_ but it is more difficult to read.

* Visually locating the closing curly brace buried in HTML tags is challenging:

```html5
<p>
    <?php if($msgCount > 0) { ?>
        You have $msgCount new messages.
    <?php } else { ?>
        No messages...  Go enjoy your day!
    <?php } ?>
</p>
```

---

### Template Example

<small style="font-size: 85%;">The following code is in the template file <tt>playlist_page.php</tt>:</small>

```html5
<!DOCTYPE html>
<html>
  <head><title>Playlist Manager</title></head>
  <body>
    <?php include($formTemplateFileName); ?>
    <hr>
    <section id='playlist'>
    <?php if(count($playlist) > 0): ?>
        <?php foreach($playlist as $track): ?>
            <article class='track'>
                <i><?= $track->title ?></i> 
                - <?= $track->artist ?> 
                [<?= $track->album ?>]
            </article>
        <?php endforeach; ?>
    <?php else: ?>
        No tracks in playlist.
    <?php endif; ?>
    </section>
  </body>
</html>
```

---

### Template Example

Now, your View object just needs to prepare the proper variables and pass the template file through the PHP interpreter:

```php
// Set variables required by the template:
$formTemplateFileName = 'playlist_form.php';
$playlist = [... code here to fill playlist ...]
// Now include the template, buffer result 
// and send it all at once when complete.
ob_start();                     // start buffer
require('playlist_page.php');   // parse the template
ob_end_flush();                 // flush buffer
```

<small style="font-size: 80%;">You will want to read documentation on the **output control** functions `ob_start()`, `ob_end_flush()`, etc.:<br>http://php.net/manual/en/ref.outcontrol.php</small>