# Controllers

Instead of defining all of your route-level logic in a single `plugin/routes.php` file, you may wish to organize this behavior using Controller classes. Controllers can group related route logic into a class and are typically stored in the `plugin/controllers` directory.

All controllers should extend the `BaseController` class. Here is an example of a basic controller class:



	class UserController extends Herbert\Framework\BaseController {

		/**
		* Show the profile for the given user.
		*/
		public function showProfile($id)
		{
			$user = User::find($id);

			return $this->view->render('user/profile', ['user' => $user]);

		}
	}

Now, we can route to this controller action like so:

	$plugin->route->get([
		'as'   => 'userShowProfile',
		'uri'  => 'user/:id'
	], 'UserController@showProfile');
