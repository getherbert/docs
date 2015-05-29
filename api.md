# API


API is a class that is exposed to the developer using your plugin. The developer may call your api in a page template like so:

	$myPluginApi->method();

### Naming your API

To set a name for your api to be accessed from, open `config.herbert.php` and set the value for `api`.


``` php
/**
* The APIs to auto-load.
*/
'apis' => [
	'MyPlugin' => __DIR__ . '/app/api.php'
],
```
In this case I'll update it to `myPluginApi`

``` php
/**
* The APIs to auto-load.
*/
'apis' => [
	'myPluginApi' => __DIR__ . '/app/api.php'
],
```


### Defining a method

You can define a new method in the `Api` class within `app/api.php` like so:

``` php
<?php namespace MyPlugin;

/** @var \Herbert\Framework\API $api */

use Herbert\Framework\Models\Post;

$api->add('getPost', function($id)
{
    return Post::find($id);
});
```

Then the developer could access this function as follows:

	$myPluginApi->getPost(2);


### Calling a controller with your method

Your api method may just be a wrapper for a controller method like so:

``` php
<?php namespace MyPlugin;

/** @var \Herbert\Framework\API $api */

use MyPlugin\Controllers\PostController;

$api->add('getPost', function($id)
{
    return (new PostController)->getPost($id);
});

```
