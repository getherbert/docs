# Helper

You may have noticed the `Helper` class being used on Enqueue and Panels to include assets from your plugin. At first this may see a little weird compared to older versions of Herbert where you could do both:

```
'src' => '/js/post.js'
'src' => '//maxcdn.bootstrapcdn.com/bootstrap/3.3.1/css/bootstrap.min.css'
```
Now that `Herbert\Framework` is only loaded once even if there are multiple plugins built on Herbert active, we've had to move path and url logic to each plugin. This is where the `Helper` class comes in. The following is an example (seen in `routes.php`) use of `Helper` while in the root namespace of an app:

```
Helper::method()
```

If your not in the root namespace (for example, inside a controller), you need to add the following before calling `Helper::method()`:

```
use MyPlugin\Helper;
```

```php
<?php namespace MyPlugin\Controllers;

use MyPlugin\Helper;

class SampleController {

    public function index()
    {
      return Helper::assetUrl('/js/main.js');
    }
}
```

## Built in methods

Get a config variable

```
Helper::get('constraint');
```
Gets a path to a relative file.

```
Helper::path('/my/file.txt');
```
Gets a path to a relative asset in `resources/assets`
```
Helper::asset('/js/main.js');
```
Gets a url to a relative asset in `resources/assets`
```
Helper::assetUrl('/js/main.js');
```
