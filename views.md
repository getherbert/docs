# Views

Instead of defining all of your html inside in your controller, you may wish to organize this in a template file. Referred to as a `views` and stored in the `resources/views` directory. Views are powered by Twig templating language. You can read more about it at: http://twig.sensiolabs.org/

Here is an example of a basic view:

	<!DOCTYPE html>
	<html>
		<head>
			<title>My Webpage</title>
		</head>
		<body>
			<h1>{{ title }}</h1>
			<p>{{ content }}</p>
		</body>
	</html>

Now, if we save the view at `resources/views/demo/example.twig`. We can call this view from our controller like so:

	return view('@MyPlugin/demo/example.twig', [
		'title'   => 'My Demo',
		'content' => 'Congrats on your demo view.'
	]);
