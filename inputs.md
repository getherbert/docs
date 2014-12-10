# Inputs

- [Basic Inputs](#basic-inputs)
- [PUT & DELETE Inputs](#put-inputs)

<a name="basic-inputs"></a>
## Basic Inputs

You may access all user input with a few simple methods. You do not need to worry about the HTTP verb when dealing with `GET` and `POST`.

> **Note:**  When inside a controller the `$plugin` class is accessed by `$this`.

### Retrieving An Input Value

	$name = $plugin->http->get('name');

### Retrieving A Default Value If The Input Value Is Absent

	$name = $plugin->http->get('name', 'Sally');

### Determining If An Input Value Is Present

	if ( $plugin->http->has('name') )
	{
		//
	}

### Getting All Input For The Request

	$input = $plugin->http->all();

<a name="put-inputs"></a>
## PUT & DELETE Inputs

Support for `PUT` & `DELETE` is limited to get all methods.

### Getting All Input For The PUT

	$input = $plugin->http->put();

### Getting All Input For The DELETE

	$input = $plugin->http->delete();
