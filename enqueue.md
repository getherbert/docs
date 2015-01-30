# Enqueue

- [Basic](#basic)
- [Filter by Panel](#filter-panel)
- [Filter by Hook](#filter-hook)
- [Filter by Post, Pages and Categories](#filter-post)
- [Filter by Archive or Search](#filter-archive)
- [Filter by Post Type](#filter-post-type)

<a name="basic"></a>
## Basic

Enqueue is the process of how WordPress loads Scripts and Styles for your plugin. It could be a piece of javascript that is required on an certain admin page or on every post. Enqueue you must supply a Source and Name. The Source is relative to your `plugin/assets` folder.

> **Note:**  Enqueue doesn't work on Routes. You must supply them using standard `link` and `script` tags.


#### Enqueue on all front-end pages

	$plugin->enqueue->front([
		'as'  => 'postsJS',
		'src' => '/js/post.js',
	]);


#### Enqueue on all admin pages

	$plugin->enqueue->admin([
		'as'  => 'adminCSS',
		'src' => '/css/admin.css',
	]);

#### Enqueue on all login pages

	$plugin->enqueue->login([
		'as'  => 'loginJS',
		'src' => '/js/login.js',
	]);

#### Setting a source to be included in the footer

	$plugin->enqueue->login([
		'as'  => 'loginJS',
		'src' => '/js/login.js',
	], 'footer');

#### Using a source from http/cdn

	$plugin->enqueue->front([
		'as'  => 'bootstrapCSS',
		'src' => '//maxcdn.bootstrapcdn.com/bootstrap/3.3.1/css/bootstrap.min.css',
	]);



<a name="filter-panel"></a>
## Filter by Panel

Its unlikely that you would want to load a source on every panel therefore you can use filters to set it on specific panel.

#### Enqueue on all your panels

	$plugin->enqueue->admin([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'panel' => '*' ]
	]);

#### Enqueue on one specific panel

	$plugin->enqueue->admin([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'panel' => 'mainPanel' ]
	]);

#### Enqueue on more than one specific panel

	$plugin->enqueue->admin([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'panel' => ['mainPanel', 'subPanel'] ]
	]);


<a name="filter-hook"></a>
## Filter by Hook

Filtering by WordPress standard panels is referred to as Hooks


#### Enqueue on one specific hook

	$plugin->enqueue->admin([
		'as'     => 'someJS',
		'src'    => '/js/login.js',
		'filter' => [ 'hook' => 'edit.php' ]
	]);

#### Enqueue on more than one specific hook

	$plugin->enqueue->admin([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'hook' => ['post-new.php', 'edit.php'] ]
	]);


<a name="filter-post"></a>
## Filter by Post, Pages and Categories

Filtering by Post, Pages and Categories work the same, they accept IDs, Name or Slugs:


#### Enqueue on all pages

	$plugin->enqueue->front([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'page' => '*' ]
	]);

#### Enqueue on one specific post

	$plugin->enqueue->front([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'post' => '23' ]
	]);

#### Enqueue on more than one specific category

	$plugin->enqueue->front([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'category' => ['12', '14'] ]
	]);

<a name="filter-archive"></a>
## Filter by Archive or Search

Filtering by Archive or Search only take the `*` input.

#### Enqueue on any search page

	$plugin->enqueue->front([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'search' => '*' ]
	]);

#### Enqueue on any archive page

	$plugin->enqueue->front([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'archive' => '*' ]
	]);

<a name="filter-post-type"></a>
## Filter by Post Type

Filtering by Post Type only accepts Slugs

#### Enqueue on one specific post type

	$plugin->enqueue->front([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'postType' => 'movies' ]
	]);

#### Enqueue on more than one specific post type

	$plugin->enqueue->front([
		'as'     => 'someJS',
		'src'    => '/js/some.js',
		'filter' => [ 'postType' => ['movies', 'games'] ]
	]);
