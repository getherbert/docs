# Routes

- [Basic Routing](#basic-routing)
- [Route Parameters](#route-parameters)
- [Routing To Controllers](#routing-to-controllers)

<a name="basic-routing"></a>
## Basic Routing

Routes for your plugin will be defined in the `plugin/routes.php` file. Herbert routes consist of a Name, URI and a Closure callback. The URI will be appended to the site url, for example: `http://example.com/simple`

#### Basic GET Route

	$plugin->route->get([
		'as'   => 'simpleRoute',
		'uri'  => '/simple'
	], function() {
		return 'Hello World';
	});


#### Basic POST Route

	$plugin->route->post([
		'as'   => 'simpleRoute',
		'uri'  => '/simple'
	], function() {
		return 'Hello World';
	});


#### Support for PUT & DELETE

Most browsers don't support `PUT` & `DELETE` yet so its recommended you avoid using these methods.

	$plugin->route->put();
	$plugin->route->delete();

#### Accessing Framework methods within the Closure

	$plugin->route->get([
		'as'   => 'simpleRoute',
		'uri'  => '/simple'
	], function() use ($plugin) {
		return $plugin->response->json(['hello' => 'world']);
	});

<a name="route-parameters"></a>
## Route Parameters

You can set route parameters in your URI by defining as `:param`. These parameters then be accessed by your Closure or Controller as `$param`

	$plugin->route->get([
		'as'   => 'userProfile',
		'uri'  => '/user/:id'
	], function($id) {
		return 'User ' . $id;
	});

<a name="routing-to-controllers"></a>
## Routing To Controllers

Herbert allows you to not only route to Closures, but also to controller classes, visit the documentation on [Controllers](/controllers) for more details.

	$plugin->route->get([
		'as'   => 'userProfile',
		'uri'  => '/user/:id'
	], 'UserController@profile');
