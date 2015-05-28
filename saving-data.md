# Saving Data

Herbert pulls in Laravels Eloquent ORM but not all plugins will need this so if you plan to save very little information then you will want to look into [WordPress Options Mechanism](http://codex.wordpress.org/Writing_a_Plugin#Saving_Plugin_Data_to_the_Database).

## Eloquent ORM

We recommend reading the docs on [Eloquent](http://laravel.com/docs/4.2/eloquent) & [Schema](http://laravel.com/docs/4.2/schema). Below is quick overview.


### Creating a Table

	use Illuminate\Database\Capsule\Manager as Capsule;

	Capsule::schema()->create('orders', function($table)
	{
		$table->increments('id');
		$table->string('title');
	});

### Dropping a Table

	use Illuminate\Database\Capsule\Manager as Capsule;

	Capsule::schema()->dropIfExists('orders');

### Create Model for Table

Models are typically stored in the `app/Models` directory. Below we create `Orders.php`

``` php
<?php namespace MyPlugin\Models;

use Illuminate\Database\Eloquent\Model as Eloquent;

class Order extends Eloquent {
	protected $fillable = ['title'];
	public $timestamps = false;
}
```


### Create Record

	Order::create(['title' => 'Wii U']);

### Get first record and update it

	$order = Order::first();
	$order->title = 'Playstation 4';
	$order->save();


## WordPress Models

To make your life easier we've include some Models to help you work with the standard WordPress tables. These include:

``` php
Herbert\Framework\Models\Comment;
Herbert\Framework\Models\CommentMeta;
Herbert\Framework\Models\Option;
Herbert\Framework\Models\Post;
Herbert\Framework\Models\PostMeta;
Herbert\Framework\Models\Taxonomy;
Herbert\Framework\Models\Term;
```
An example of using one of these to get a Post by id.

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
