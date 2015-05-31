# Getting Started

> **Note:**  These docs are going through a rewrite and should be up to date by end of 31st May.

Welcome, Herbert is a plugin framework for WordPress. We believe the current approach to building plugins is unorganised and difficult to understand. It makes working in teams or taking over from a previous developer time consuming. Its early days for Herbert but our aim is to solve this.

## Requirements

Herbert requires [Composer](https://getcomposer.org/). Please make sure it's installed before continuing.  

#### Installing Composer on Linux or Mac OS X

```
$ curl -sS https://getcomposer.org/installer | php
$ sudo mv composer.phar /usr/local/bin/composer
```

#### Installing on Windows

Download the installer from getcomposer.org/download, execute it and follow the instructions.

## Installation

Download the latest version of the Herbert framework and extract its contents into a directory on your server. Next, in the root of your plugin, run the php composer.phar install (or composer install) command to install all of the framework's dependencies. This process requires Git to be installed on the server to successfully complete the installation.

## Working with WordPress

Developing a plugin using Herbert should happen outside of your WordPress install. As in:

	//WordPress Install
	/path/to/sites/wordpress/wp-content/plugins/plugin-name

	//Plugin
	/path/to/projects/plugin-name

 To achieve this we use a Symbolic Link.

	ln -s /path/to/projects/plugin-name /path/to/sites/wordpress/wp-content/plugins/plugin-name

## Naming your Plugin

Open the `plugin.php` and you will see a comment at the top where you set several settings. As standard it looks like so:


	/**
	* @wordpress-plugin
	* Plugin Name:       My Plugin
	* Plugin URI:        http://plugin-name.com/
	* Description:       A plugin.
	* Version:           1.0.0
	* Author:            Author
	* Author URI:        http://author.com/
	* License:           MIT
	*/

## Namespacing your Plugin

To avoid conflicts with other plugins or the WordPress core its important to set a [namespace](http://php.net/manual/en/language.namespaces.php). To get started lets open up `composer.json` and find the `autoload` section. As standard it looks like:

``` javascript
"autoload": {
    "psr-4": {
      "MyPlugin\\": "app/"
    }
  }
```
Now let's update `MyPlugin` with your namespace. Generally your plugin name without spaces, for example: Our plugin called `Social Icons (pro)` would become `SocialIconsPro`. Now the autoload section would look like:

``` javascript
"autoload": {
    "psr-4": {
      "SocialIconsPro\\": "app/"
    }
  }
```
We need to tell composer that we've made this change so in your plugin root run `composer dump-autoload`. Now at the top of each of the following files:

```
app/
├── Helper.php
├── api.php
├── enqueue.php
├── panels.php
├── routes.php
├── shortcodes.php
├── widgets.php
```


We'll update their namespace from `MyPlugin` to `SocialIconsPro` by changing this line:

``` php
<?php namespace MyPlugin;
```
Update to:

``` php
<?php namespace SocialIconsPro;
```

And lastly lets open the config file `herbert.config.php` and change update four `MyPlugins` to your namespace.

``` php
/**
* The routes to auto-load.
*/
'routes' => [
  'MyPlugin' => __DIR__ . '/app/routes.php'
],

/**
* The panels to auto-load.
*/
'panels' => [
  'MyPlugin' => __DIR__ . '/app/panels.php'
],

/**
* The APIs to auto-load.
*/
'apis' => [
  'MyPlugin' => __DIR__ . '/app/api.php'
],

/**
* The view paths to register.
*
* E.G: 'MyPlugin' => __DIR__ . '/views'
* can be referenced via @MyPlugin/
* when rendering a view in twig.
*/
'views' => [
	'MyPlugin' => __DIR__ . '/resources/views'
],
```

Update to:

``` php
/**
* The routes to auto-load.
*/
'routes' => [
  'SocialIconsPro' => __DIR__ . '/app/routes.php'
],

/**
* The panels to auto-load.
*/
'panels' => [
  'SocialIconsPro' => __DIR__ . '/app/panels.php'
],

/**
* The APIs to auto-load.
*/
'apis' => [
  'SocialIconsPro' => __DIR__ . '/app/api.php'
],

/**
* The view paths to register.
*
* E.G: 'MyPlugin' => __DIR__ . '/views'
* can be referenced via @MyPlugin/
* when rendering a view in twig.
*/
'views' => [
	'SocialIconsPro' => __DIR__ . '/resources/views'
],

```
