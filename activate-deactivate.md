# Activate & Deactivate

When your plugin is activated or deactivated you may need to carry out some tasks. This could checking requirements or handling database tables.


### Activate

Activate actions should be defined in `plugin/activate.php`. They will accept a Closure or Controller method


	$plugin->general->activate( function() use ($plugin) {

		Capsule::schema()->create('orders', function($table)
		{
			$table->increments('id');
			$table->string('title');
		});

	});


### Deactivate

Deactivate actions should be defined in `plugin/deactivate.php`. They will accept a Closure or Controller method

	$plugin->general->deactivate('DatabaseController@dropOrders');
