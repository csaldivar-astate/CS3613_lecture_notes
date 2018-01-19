# Slim Framework Supplement
## Documentation Addendum

---

## Read the Docs!

Before reading this information, you should be familiar with the Slim Framework official documentation:

http://docs.slimframework.com/

Really -- go read it.

---

## Route Targets

Slim allows route targets to be specified as inline _anonymous functions_ (this is all that is shown in the official documentation). **However,** Slim also allows route targets to be specified as the _name_ of a function (or method) that should be called (as type `string`):

```php
// Route to a controller for Book that has a static method named `show`
// The method will receive one arguement: the `id`.
$app->get('/books/:id', '\Controllers\Book::show');

// Route POST data to a `create` method on the Controller class `Book`:
$app->post('/books', '\Controllers\Book::create');
```

---

## URL Rewriting

Add a file named `.htaccess` (_notice the leading dot_) to the same directory that contains your `index.php` routing controller.  The file should contain the following:

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^ index.php [QSA,L]
```

---

## Slim App in Route Targets

A route target may receive arguments from the route if there were any parameters specified.

You may also want access to the Slim application instance itself.  You can get this with the following line:

```php
$app = \Slim\Slim::getInstance();
```

Slim route handlers recieve the Request and Response (PSR-7) objects, so you can get data as follows:

```php
// Get the user's name from POST data.
$requestPostPutVars = $request->getParsedBody();
$userName = $requestPostPutVars['name'];
```

---

## Middleware

Slim Middleware is designed to allow "filtering" the request in some way before producing the final View at the route target.  Each middleware function receives the current Route as an argument:

```php
function showRoute($request, $response, $next) {
    echo "Current route is " . $request->getAttribute('route')->getName();
    return $next($request, $response);
};

$app->get('/info', 'Views\Foo::show')->add('showRoute');
```

You can use the same process as in the target to get the application object.

---

## Route Parameters in Middleware

<small style="font-size: 95%;">You can get parameters from the route in middleware exactly like you can in a Route:

* `getParam( 'param-name' )` - gets a single parameter by name
* `getParams()` - returns an array with all parameters

```php
function showParams($request, $response, $next) {
    // Get "example" from POST data
    $requestPostPutVars = $request->getParsedBody();
    $param = $requestPostPutVars['example'];
    echo "'example' is: $param. <br>\n";
    echo "All params: <br>\n";
    foreach($requestPostPutVars as $name => $value){
        echo "name: $name -- value: $value <br>\n";
    }
}

$app->get('/:example/:route/:params', 
          'Views\Foo::show')->add('showParams');
```
</small>

