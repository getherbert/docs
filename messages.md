# Messages

Messages are used to show a User of the plugin some information. They have three types: `success`, `warning` or `error`. These messages will be displayed at the top of the WordPress admin area. Messages can be used anywhere in the plugin by referencing `Notifier`.

``` php
use Herbert\Framework\Notifier;
```

### Adding a Success Message

	Notifier::success('Finished installing');


### Adding a Warning Message

	Notifier::warning('We recommend clearing your cache');

### Adding a Error Message

	Notifier::error('Something has gone wrong');
