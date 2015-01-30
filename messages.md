# Messages

Messages are used to show a User of the plugin some information. They have three types: `success`, `warning` or `error`. These messages will be displayed at the top of the WordPress admin area. Messages can be used anywhere in the plugin.

### Adding a Success Message

	$plugin->message->success( $plugin->name . ': has finished installing.');


### Adding a Warning Message

	$plugin->message->warning('We recommend clearing your cache');

### Adding a Error Message

	$plugin->message->error('Something has gone wrong');
