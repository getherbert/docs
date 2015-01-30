# Saving Data

Herbert pulls in Laravels Eloquent ORM but not all plugins will need this so if you plan to save very little information then you will want to look into [WordPress Options Mechanism](http://codex.wordpress.org/Writing_a_Plugin#Saving_Plugin_Data_to_the_Database). If thats the case then you should disable Eloquent:

Open `config.php` and set the following line to `false`

	'eloquent' => true


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

Models are typically stored in the `plugin/models` directory. Below we create `Orders.php`

	use Illuminate\Database\Eloquent\Model as Eloquent;

	class Order extends Eloquent {
		protected $fillable = ['title'];
		public $timestamps = false;
	}


### Create Record

	Order::create(['title' => 'Wii U']);

### Get first record and update it

	$order = Order::first();
	$order->title = 'Playstation 4';
	$order->save();
