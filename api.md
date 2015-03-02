# API


API is a class that is exposed to the developer using your plugin. It extends the `BaseController` like any other controller in your plugin. The developer may call your api in a page template like so:

	$myPluginApi->method();

### Naming your API

To set a name for your api to be accessed from, open `config.php` and set the value for `api`.


	'api' => 'myPluginApi'


### Defining a method

You can define a new method in the `Api` class within `plugin/api.php` like so:


	class Api extends BaseController {

		/**
		* Show username for the given user.
		*/
		public function showUsername($id)
		{
			$user = User::find($id);

			return $user->username;
		}
	}

Then the developer could access this function as follows:

	$myPluginApi->showUsername(2);


### Calling a controller with your method

Your api method may just be a wrapper for a controller method like so:

	class Api extends BaseController {

		/**
		* Show username for the given user.
		*/
		public function showUsername($id)
		{
			$username = $this->controller->fetch('UserController@getUsername', ['id' => 2]);

			return $username;
		}
	}
