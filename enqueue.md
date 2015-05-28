# Enqueue

- [Basic](#basic)
- [Filter by Panel](#filter-panel)
- [Filter by Hook](#filter-hook)
- [Filter by Post, Pages and Categories](#filter-post)
- [Filter by Archive or Search](#filter-archive)
- [Filter by Post Type](#filter-post-type)

<a name="basic"></a>
## Basic

Enqueue is the process of how WordPress loads Scripts and Styles for your plugin. It could be a piece of javascript that is required on an certain admin page or on every post. Enqueue you must supply a Source and Name. The Source takes a URL, to use a relative path from `app/assets` folder we wrap with the `Helper::assetUrl()` function.

To read more about the `Helper` class [here](/$branch/hepler)

> **Note:**  Enqueue doesn't work on Routes. You must supply them using standard `link` and `script` tags.


#### Enqueue on all front-end pages

	$enqueue->front([
		'as'  => 'postsJS',
		'src' => Helper::assetUrl('/js/post.js')
	]);


#### Enqueue on all admin pages

	$enqueue->admin([
		'as'  => 'adminCSS',
		'src' => Helper::assetUrl('/css/admin.css'),
	]);

#### Enqueue on all login pages

	$enqueue->login([
		'as'  => 'loginJS',
		'src' => Helper::assetUrl('/js/login.js'),
	]);

#### Setting a source to be included in the footer

	$enqueue->login([
		'as'  => 'loginJS',
		'src' => Helper::assetUrl('/js/login.js'),
	], 'footer');

#### Using a source from http/cdn

	$enqueue->front([
		'as'  => 'bootstrapCSS',
		'src' => '//maxcdn.bootstrapcdn.com/bootstrap/3.3.1/css/bootstrap.min.css',
	]);



<a name="filter-panel"></a>
## Filter by Panel

Its unlikely that you would want to load a source on every panel therefore you can use filters to set it on specific panel.

#### Enqueue on all your panels

	$enqueue->admin([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'panel' => '*' ]
	]);

#### Enqueue on one specific panel

	$enqueue->admin([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'panel' => 'mainPanel' ]
	]);

#### Enqueue on more than one specific panel

	$enqueue->admin([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'panel' => ['mainPanel', 'subPanel'] ]
	]);


<a name="filter-hook"></a>
## Filter by Hook

Filtering by WordPress standard panels is referred to as Hooks


#### Enqueue on one specific hook

	$enqueue->admin([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/login.js'),
		'filter' => [ 'hook' => 'edit.php' ]
	]);

#### Enqueue on more than one specific hook

	$enqueue->admin([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'hook' => ['post-new.php', 'edit.php'] ]
	]);


<a name="filter-post"></a>
## Filter by Post, Pages and Categories

Filtering by Post, Pages and Categories work the same, they accept IDs, Name or Slugs:


#### Enqueue on all pages

	$enqueue->front([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'page' => '*' ]
	]);

#### Enqueue on one specific post

	$enqueue->front([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'post' => '23' ]
	]);

#### Enqueue on more than one specific category

	$enqueue->front([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'category' => ['12', '14'] ]
	]);

<a name="filter-archive"></a>
## Filter by Archive or Search

Filtering by Archive or Search only take the `*` input.

#### Enqueue on any search page

	$enqueue->front([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'search' => '*' ]
	]);

#### Enqueue on any archive page

	$enqueue->front([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'archive' => '*' ]
	]);

<a name="filter-post-type"></a>
## Filter by Post Type

Filtering by Post Type only accepts Slugs

#### Enqueue on one specific post type

	$enqueue->front([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'postType' => 'movies' ]
	]);

#### Enqueue on more than one specific post type

	$enqueue->front([
		'as'     => 'someJS',
		'src'    => Helper::assetUrl('/js/some.js'),
		'filter' => [ 'postType' => ['movies', 'games'] ]
	]);
