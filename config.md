# Config

- [Constraint](#constraint)
- [Extend](#extend)
- [Namespacing](#namespacing)
- [Flat Files](#flat-files)

<a name="constraint"></a>
## Constraint

The constraint section is very important. As the Herbert/Framework is only included once, even when multiple plugins are using Herbert. To would around this you set the minimum version that your plugin will support. If we had three plugins installed:

```
PluginOne -> Herbert 0.9
PluginTwo -> Herbert 1.1
PluginThree -> Herbert 1.0
```
If either PluginOne or PluginTwo have constraint higher than 0.9 the user will be warned that the plugins won't work together and try updating to the latest version.

<a name="extend"></a>
## Extend

You can add your own variables to the Config file and easily retrieve them later. Open up the `herbert.config.php` and two new variables.

``` php
return [

    /**
     * My plugin name
     */

    'pluginName' => 'Social Icons Pro',

    /**
     * My table prefix
     */

    'prefix' => 'sip_',

    /**
     * The Herbert version constraint.
     */
    'constraint' => '~0.9',

    /**
```

Then throughout your plugin you can use the `Helper` class to retrieve them.

``` php
$pluginName = Helper::get('pluginName');
```

``` php
$tablePrefix = Helper::get('prefix');
```
<a name="namespacing"></a>
## Namespacing

During the Getting Started section there is four sections we ask you set your namespace for. They use the following format:

``` php
'type' => [
    'Namespace' => 'file.php'
],
```

#### Routes

The routes section lets you define any files you wish to pull in that will have access to `$router`. They also require a namespace (different or the same). Below is an example:

``` php
'routes' => [
    'SocialIconsProGeneral' => __DIR__ . '/app/routes.general.php',
    'SocialIconsProApi' => __DIR__ . '/app/routes.api.php'
],
```
And in each file we define a route.

`app/routes.general.php`

``` php
$router->get([
	'as'   => 'info',
	'uri'  => '/sip/info',
	'uses' => __NAMESPACE__ . '\Controllers\GeneralController@info'
]);
```

`app/routes.api.php`

``` php
$router->get([
	'as'   => 'info',
	'uri'  => '/sip/api/info',
	'uses' => __NAMESPACE__ . '\Controllers\ApiController@info'
]);
```
Now if we wanted to get url of the first route we do:

``` php
route_url('SocialIconsProGeneral::info');
```
And for the second route.

``` php
route_url('SocialIconsProApi::info');
```

#### Panels

The panel section lets you define any files you wish to pull in that will have access to `$panel`. They also require a namespace (different or the same). Below is an example:

``` php
'panels' => [
    'SocialIconsProGeneral' => __DIR__ . '/app/panels.general.php',
    'SocialIconsProApi' => __DIR__ . '/app/panels.api.php'
],
```
And in each file we define a panel.

`app/panels.general.php`

``` php
$panel->add([
    'type'   => 'sub-panel',
    'parent' => 'main',
    'as'     => 'info',
    'title'  => 'General Info',
    'slug'   => 'myplugin-general-info'
    'uses'   => __NAMESPACE__ . '\Controllers\GeneralController@info'
]);
```

`app/panels.api.php`

``` php
$panel->add([
    'type'   => 'sub-panel',
    'parent' => 'main',
    'as'     => 'info',
    'title'  => 'Api Info',
    'slug'   => 'myplugin-api-info'
    'uses'   => __NAMESPACE__ . '\Controllers\ApiController@info'
]);
```
Now if we wanted to get url of the first route we do:

``` php
panel_url('SocialIconsProGeneral::info');
```
And for the second route.

``` php
panel_url('SocialIconsProApi::info');
```

#### Api

The api section lets you define any files you wish to pull in that will have access to `$api`. They also require a namespace (different or the same). Below is an example:

``` php
'apis' => [
    'socialIconsProTwitter' => __DIR__ . '/app/api.twitter.php',
    'socialIconsProFacebook' => __DIR__ . '/app/api.facebook.php'
],
```
And in each file we define a method.

`app/api.twitter.php`

``` php
$api->add('extend', function($id)
{
    //some awesome code
});
```

`app/api.facebook.php`

``` php
$api->add('extend', function($id)
{
    //some awesome code
});
```
Now the user of your plugin would access the apis by:

``` php
$socialIconsProTwitter->extend();
$socialIconsProFacebook->extend();
```

And when using with shortcodes

``` php
$shortcode->add(
    'SipTwitterExtend',
    'socialIconsProTwitter::extend'
);
```

``` php
$shortcode->add(
    'SipFacebookExtend',
    'socialIconsProFacebook::extend'
);
```

#### Views

Views works differently to the other three. It acts as shorthand for a directory.

``` php
'views' => [
    'SipAdmin' => __DIR__ . '/resources/views/admin',
    'SipEmails' => __DIR__ . '/resources/views/emails',
],
```
And you would use them like so:

``` php
return view('@SipAdmin/example.twig');
return view('@SipEmails/example.twig');
```

<a name="flat-files"></a>
## Flat Files

Flat files are files that can have any purpose while having access to the `$container`. And example of one is the `customPostTypes.php`. You can add more into the require section of the config. Lets add a file for doing some logic for when a post is trashed.

Lets create file:

```
app/hooks/postIsTrashed.php
```

And lets at in the config

``` php
'requires' => [
    __DIR__ . '/app/customPostTypes.php',
    __DIR__ . '/app/hooks/postIsTrashed.php'
],
```

And in the file

``` php
<?php

add_action( 'wp_trash_post', function()
{
  //some code to say backup the post
});
```
