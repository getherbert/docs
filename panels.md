# Panels

- [Main Panels](#main-panels)
- [Subpanels](#subpanels)
- [WordPress Subpanels](#wp-subpanels)

<a name="main-panels"></a>
## Main Panels

Panels (or menus) for your plugin will be defined in the `plugin/panels.php` file. Herbert panels refer to an option in left sidebar of WordPress admin area. They consist of a Type, Name, Title, Slug and a Closure callback. The Slug will be appended to the site admin url, for example: `http://example.com/wp-admin/admin.php?page=myplugin-index`


#### Main Panel using Closure

	$plugin->panel->add([
		'type'   => 'panel',
		'as'     => 'mainPanel',
		'title'  => 'My Plugin',
		'slug'   => 'myplugin-index'
	], function() use ($plugin) {
		return 'Hello World';
	});



#### Main Panel using a Controller

	$plugin->panel->add([
		'type'   => 'panel',
		'as'     => 'mainPanel',
		'title'  => 'My Plugin',
		'slug'   => 'myplugin-index'
	], 'AdminController@index');


#### Supplying an Icon
Panels support four different icon methods, each detailed below:

```
'dashicons-media-audio' //Dashicons Class
'none' //Styleable Div
'/img/icon.png' //Relative Path
'//site.com/icon.png' //HTTP
```

Below is an example using `dashicons`

	$plugin->panel->add([
		'type'   => 'panel',
		'as'     => 'mainPanel',
		'title'  => 'My Plugin',
		'slug'   => 'myplugin-index',
		'icon'   => 'dashicons-media-audio'
	], 'AdminController@index');

<a name="subpanels"></a>
## Subpanels

If you require more than one panel for your plugin you may decided to add them as subpanel:

```
My Plugin
├── Configure
├── Update
```

To add a subpanel, you set its Type to `subpanel` and supply a Parent Name.

	$plugin->panel->add([
		'type'   => 'subpanel',
		'parent' => 'mainPanel',
		'as'     => 'configure',
		'title'  => 'Configure',
		'slug'   => 'myplugin-configure'
	], 'AdminController@configure');

#### Renaming the Root Subpanel

You will notice if you add the first subpanel that WordPress will automatically insert a subpanel named the same as parent:

```
My Plugin
├── My Plugin
├── Configure
```

To rename this just supply the Name of the parent and the new Title

	$plugin->panel->renameDefaultSubpanel([
		'default' => 'mainPanel',
		'title'   => 'General'
	]);

<a name="wp-subpanels"></a>
## WordPress Subpanels

If you require a subpanel under one of the standard WordPress panels, for example:

```
Dashboard
├── Home
├── Updates
├── Your Subpanel
```

To add a WordPress subpanel, you set its Type to `wp-subpanel` and supply a Parent Name.

	$plugin->panel->add([
		'type'   => 'wp-subpanel',
		'parent' => 'index.php',
		'as'     => 'dashboardSubpanel',
		'title'  => 'Your Subpanel'
		'slug'   => 'myplugin-dashboard'
		], 'AdminController@dashboard');

There is 12 different types of WordPress panels which you can supply as a Parent Name:

```
Dashboard: 'index.php'
Posts: 'edit.php'
Media: 'upload.php'
Links: 'link-manager.php'
Pages: 'edit.php?post_type=page'
Comments:'edit-comments.php'
Custom Post Types: 'edit.php?post_type=your_post_type'
Appearance: 'themes.php'
Plugins: 'plugins.php'
Users: 'users.php'
Tools: 'tools.php'
Settings: 'options-general.php'
```
