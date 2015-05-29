# Shortcodes

Shortcodes are for non-technical users to access some function of your plugin within the WordPress content editor. Therefore adding a shortcode is generally just a reference to API method. Shortcodes consist of a Name, API Call and Argument Name Array (more on this later) and are defined in `app/shortcodes.php`

### Adding a Basic Shortcode

	$shortcode->add('UserProGetUsername', 'getUsername');

``` php
$shortcode->add(
    'MyPluginShowPostName',
    '@myPluginApi\showPostName'
);
```


This would then be accessed by the shortcode like so:

	[MyPluginShowPostName]


### Handling Argument Names

Unfortunately WordPress doesn't support camel case in shortcode arguments therefore you can supply an array to rename them.


``` php
$shortcode->add(
    'MyPluginShowPostName',
    '@myPluginApi\showPostName',
    [
        'post_id' => 'postId'
    ]
);

```

This would then be accessed by the shortcode like so:

	[MyPluginShowPostName post_id=2]

With your API method:

``` php
$api->add('showPostName', function($postId)
{
    return (new PostController)->showPostName($postId);
});
```

### Using any controller method or closure

In some cases you may need to call normal controller method or do some setup before hand in a closure.

``` php
$shortcode->add(
    'MyPluginShowPostName',
    __NAMESPACE__ . '\Controllers\PostController@showPostName',
    [
        'post_id' => 'postId'
    ]
);
```
Or using a closure
``` php
$shortcode->add(
    'MyPluginShowPostName',
    function($postId)
    {
        //Some awesome code
    },
    [
        'post_id' => 'postId'
    ]
);

```
