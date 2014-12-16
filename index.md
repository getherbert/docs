# Getting Started

Welcome, Herbert is a plugin framework for Wordpress. We believe the current approach to building plugins is unorganised and difficult to understand. It makes working in teams or taking over from a previous developer time consuming. Its early days for Herbert but our aim is to solve this.


## Installation

Once Composer is installed, download the latest version of the Herbert framework and extract its contents into a directory on your server. Next, in the root of your plugin, run the php composer.phar install (or composer install) command to install all of the framework's dependencies. This process requires Git to be installed on the server to successfully complete the installation.

## Working with Wordpress

Developing a plugin using Herbert should happen outside of your Wordpress install. As in:

	//Wordpress Install
	/path/to/sites/wordpress/wp-content/plugins/plugin-name

	//Plugin
	/path/to/projects/plugin-name

 To achieve this we use a Symbolic Link.

	ln -s /path/to/projects/plugin-name /path/to/sites/wordpress/wp-content/plugins/plugin-name

## Naming your Plugin

Open the 'plugin.php' and you will see a comment at the top where you set several settings. As standard it looks like so:


	/**
	* @wordpress-plugin
	* Plugin Name:       Plugin Name
	* Plugin URI:        http://plugin-name.com/
	* Description:       A plugin.
	* Version:           1.0.0
	* Author:            Author
	* Author URI:        http://author.com/
	* License:           MIT
	*/
