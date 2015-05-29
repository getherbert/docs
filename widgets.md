# Widgets

Widget are typically stored in the `app/Widgets` directory. Once ready to register them with WordPress you can do so in `app/widgets.php`.

When defining a widget it must extend the `WP_Widget` class. Here is an example of a basic widget class:


 `app/Widgets/MyWidget.php`

``` php
<?php namespace MyPlugin\Widgets;

class MyWidget extends \WP_Widget {

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
```

Now, we can register this widget like so:

`app/widgets.php`

	$widget->add(__NAMESPACE__ . '\Widgets\MyWidget');
