# Activate & Deactivate

When your plugin is activated or deactivated you may need to carry out some tasks. This could be checking requirements or handling database tables.


### Activate

Activate actions should be defined in `app/activate.php`. This is special type of flat file which any code is executed. You will also have access to all framework components like `$http` or `$router`.  

``` php
<?php

/** @var  \Herbert\Framework\Application $container */
/** @var  \Herbert\Framework\Http $http */
/** @var  \Herbert\Framework\Router $router */
/** @var  \Herbert\Framework\Enqueue $enqueue */
/** @var  \Herbert\Framework\Panel $panel */
/** @var  \Herbert\Framework\Shortcode $shortcode */
/** @var  \Herbert\Framework\Widget $widget */

use Illuminate\Database\Capsule\Manager as Capsule;

Capsule::schema()->create('orders', function($table)
{
	$table->increments('id');
	$table->string('title');
});

```

### Deactivate

Deactivate actions should be defined in `plugin/deactivate.php`.

``` php
<?php

/** @var  \Herbert\Framework\Application $container */
/** @var  \Herbert\Framework\Http $http */
/** @var  \Herbert\Framework\Router $router */
/** @var  \Herbert\Framework\Enqueue $enqueue */
/** @var  \Herbert\Framework\Panel $panel */
/** @var  \Herbert\Framework\Shortcode $shortcode */
/** @var  \Herbert\Framework\Widget $widget */

use Illuminate\Database\Capsule\Manager as Capsule;

Capsule::schema()->dropIfExists('orders');

```
