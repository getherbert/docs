# Routes

- [Basic Routing](#basic-routing)
- [Route Parameters](#route-parameters)
- [Routing To Controllers](#routing-to-controllers)

<a name="basic-routing"></a>
## Basic Routing

Routes for your plugin will be defined in the `app/routes.php` file. Herbert routes consist of a Name, URI and a Closure callback. The URI will be appended to the site url, for example: `http://example.com/simple`

#### Basic GET Route

``` php
$router->get([
	'as'   => 'simpleRoute',
	'uri'  => '/simple',
	'uses' => function()
	{
		return 'Hello World';
	}
]);
```

#### Basic POST Route

``` php
$router->post([
	'as'   => 'simpleRoute',
	'uri'  => '/simple',
	'uses' => function()
	{
		return 'Hello World';
	}
]);
```

#### Support for PUT & DELETE

Most browsers don't support `PUT` & `DELETE` yet so its recommended you avoid using these methods.

```
$router->put();
$router->delete();
```

#### Accessing framework components within a closure

``` php
$router->get([
	'as'   => 'simpleRoute',
	'uri'  => '/simple',
	'uses' => function(\Herbert\Framework\Http $http)
	{
		return "This route was accessed through http {$http->method()} method";
	}
]);
```

<a name="route-parameters"></a>
## Route Parameters

You can set route parameters in your URI by defining as `{param}`. These parameters then be accessed by your Closure or Controller as `$param`


``` php
$router->get([
	'as'   => 'userProfile',
	'uri'  => '/user/{id}',
	'uses' => function($id)
	{
		return "User: {$id}";
	}
]);
```

<a name="routing-to-controllers"></a>
## Routing To Controllers

Herbert allows you to not only route to closures, but also to controller classes, visit the documentation on [Controllers](/$branch/controllers) for more details.


``` php
$router->get([
	'as'   => 'userProfile',
	'uri'  => '/user/{id}',
	'uses' => __NAMESPACE__ . '\Controllers\UserController@profile'
]);
```
