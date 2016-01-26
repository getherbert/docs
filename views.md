# Views

Instead of defining all of your html inside of your controller you may wish to organize it into template files. These files, referred to as a `views`, are stored in the `resources/views` directory. Views are powered by the Twig templating language. You can read more about Twig at: http://twig.sensiolabs.org/

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

Now, if we save the view at `resources/views/demo/example.twig`, we can call it from our controller like so:

	return view('@MyPlugin/demo/example.twig', [
		'title'   => 'My Demo',
		'content' => 'Congrats on your demo view.'
	]);
