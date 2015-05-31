# Custom Post Types

Herbert doesn't do anything to abstract how you would add a custom post type. This may change in the future but now you can use the standard WordPress way. You will find a file `app/customPostTypes.php` which is a sample of where you could define a CPT. This file is flat file which you can read more about in the config section.

## CPTs the WordPress way

It's worth reading the [official documentation](https://codex.wordpress.org/Post_Types) on CPTs if your not familiar. Two other great sources are a [guide](http://www.smashingmagazine.com/2012/11/08/complete-guide-custom-post-types/) by Smashing Magazine and [CPT generator](http://generatewp.com/post-type/) from Generate WP. Below is an example of an Event CPT.


``` php
// Register Custom Post Type
function event_cpt() {

    $labels = [
        'name'                => _x( 'Events', 'Post Type General Name', 'text_domain' ),
        'singular_name'       => _x( 'Event', 'Post Type Singular Name', 'text_domain' ),
        'menu_name'           => __( 'Event', 'text_domain' ),
        'name_admin_bar'      => __( 'Event', 'text_domain' ),
        'parent_item_colon'   => __( 'Parent Event:', 'text_domain' ),
        'all_items'           => __( 'All Events', 'text_domain' ),
        'add_new_item'        => __( 'Add New Event', 'text_domain' ),
        'add_new'             => __( 'Add New', 'text_domain' ),
        'new_item'            => __( 'New Event', 'text_domain' ),
        'edit_item'           => __( 'Edit Event', 'text_domain' ),
        'update_item'         => __( 'Update Event', 'text_domain' ),
        'view_item'           => __( 'View Event', 'text_domain' ),
        'search_items'        => __( 'Search Events', 'text_domain' ),
        'not_found'           => __( 'Not found', 'text_domain' ),
        'not_found_in_trash'  => __( 'Not found in Trash', 'text_domain' ),
    ];
    $rewrite = [
        'slug'                => 'event',
        'with_front'          => true,
        'pages'               => true,
        'feeds'               => true,
    ];
    $args = [
        'label'               => __( 'event', 'text_domain' ),
        'description'         => __( 'List of Events', 'text_domain' ),
        'labels'              => $labels,
        'supports'            => array( ),
        'taxonomies'          => array( 'category', 'post_tag' ),
        'hierarchical'        => false,
        'public'              => true,
        'show_ui'             => true,
        'show_in_menu'        => true,
        'menu_position'       => 5,
        'show_in_admin_bar'   => true,
        'show_in_nav_menus'   => true,
        'can_export'          => true,
        'has_archive'         => true,
        'exclude_from_search' => false,
        'publicly_queryable'  => true,
        'rewrite'             => $rewrite,
        'capability_type'     => 'page',
    ];
    register_post_type( 'event', $args );

}

// Hook into the 'init' action
add_action( 'init', 'event_cpt', 0 );
```

## Using a Package

If you want a different way of doing it you could always use Composer to pull in a package (maybe write your own package), for example lets pull in:

https://github.com/jjgrainger/wp-custom-post-type-class

Open your `composer.json` and under require add:

```
"jjgrainger/wp-custom-post-type-class": "dev-master"
```

Run `composer install` and now you could create a CPT like so:

``` php
$people = new CPT([
    'post_type_name' => 'person',
    'singular' => 'Person',
    'plural' => 'People',
    'slug' => 'people'
]);
```

## Organise

The logic for CPTs can be pretty large and having it in all one file would most likely be difficult to manage. An example of how you manage this a little better - it's assume we have three CPTs: People, Books and Events.

Let create a folder for our CPTs.

```
app/CustomPostTypes
```

And lets create a file for People.

`app/CustomPostTypes/People.php`

``` php
<?php namespace MyPlugin\CustomPostTypes;


class People {

  public function register()
  {
    \add_action( 'init', function()
    {
      $labels = [...];
      $rewrite = [...];
      $args = [...];
      \register_post_type('event', $args);
    }
    ,0);
  }
}
```

We'd repeat for the other two CPTs so our folder would have:

```
app/CustomPostTypes/
  People.php
  Books.php
  Events.php
```
Then in `app/customPostTypes` you could do

``` php
<?php

/** @var  \Herbert\Framework\Application $container */

use MyPlugin\CustomPostTypes\People;
use MyPlugin\CustomPostTypes\Books;
use MyPlugin\CustomPostTypes\Events;

// Register People CPT
(new People)->register();

// Register Books CPT
(new Books)->register();

// Register Events CPT
(new Events)->register();

```
