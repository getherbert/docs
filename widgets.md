# Widgets

Widget are typically stored in the `plugin/widgets` directory. Once ready to register them with WordPress you can do so in `plugin/widgets.php`.

When defining a widget it must extend the `BaseWidget` class. Here is an example of a basic widget class:


	class MyWidget extends BaseWidget {

		public function __construct() {

		}

		public function widget( $args, $instance ) {
			// outputs the content of the widget
		}

		public function form( $instance ) {
			// outputs the options form on admin
		}

		public function update( $new_instance, $old_instance ) {
			// processes widget options to be saved
		}

	}


Now, we can register this widget like so:

	$plugin->widget->register('MyWidget');
