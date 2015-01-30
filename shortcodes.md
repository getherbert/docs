# Shortcodes

Shortcodes are for non-technical users to access some function of your plugin within the WordPress content editor. Therefore adding a shortcode is just a reference to API method. Shortcodes consist of a Name, API Method Name and Argument Name Array (more on this later) and are defined in `plugins/shortcodes.php`

### Adding a Basic Shortcode


	$plugin->shortcode->add('UserProGetUsername', 'getUsername');

This would then be accessed by the shortcode like so:

	[UserProGetUsername id='2']


### Handling Argument Names

Unfortunately WordPress doesn't support camel case in shortcode arguments therefore you can supply an array to rename underscore names to camel case.



	$plugin->shortcode->add('UserProGetUsername', 'getUsername', [
		'user_id' => 'userId'
	]);
