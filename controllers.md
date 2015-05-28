# Controllers

Instead of defining all of your route-level logic in a single `app/routes.php` file, you may wish to organize this behavior using Controller classes. Controllers can group related route logic into a class and are typically stored in the `app/Controllers` directory.

Don't forgot to namespace your controllers. Here is an example of a basic controller class:

 `app/Controllers/PostController.php`


```php

<?php namespace MyPlugin\Controllers;

use Herbert\Framework\Models\Post;

class PostController {

    /**
     * Show the post for the given id.
     */
    public function showPost($id)
    {
        $post = Post::find($id);

        return view('@MyPlugin/post/single.twig', ['post' => $post]);
    }
}
```

Now, we can route to this controller action like so:

``` php
$router->get([
    'as'   => 'postSingle',
    'uri'  => 'post/{id}',
    'uses' => __NAMESPACE__ . '\Controllers\PostController@showPost'
]);
```
Below is a more advanced example demonstrating how you could include the `Http` component of framework. On top of that we show you how to return different http status (in this case 404) as well as a json repsonse.

``` php
<?php namespace MyPlugin\Controllers;

use Herbert\Framework\Models\Post;
use Herbert\Framework\Http;

class PostController {

    /**
     * Show the post for the given id.
     */
    public function showPost($id, Http $http)
    {
        $post = Post::find($id);

        if(!$post)
        {
            return response('Post not found', 404);
        }

        if($http->has('json'))
        {
            return json_response($post);
        }

        return view('@MyPlugin/post/single.twig', ['post' => $post]);
    }
}

```
