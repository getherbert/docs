# Inputs


You may access all user input with a few simple methods. You do not need to worry about the HTTP verb when dealing with `GET` and `POST`.

> **Note:**  Remember to include `Herbert\Framework\Http $http`.

### Retrieving An Input Value

	$name = $http->get('name');

### Retrieving A Default Value If The Input Value Is Absent

	$name = $http->get('name', 'Sally');

### Determining If An Input Value Is Present

	if ( $http->has('name') )
	{
		//
	}

### Getting All Input For The Request

	$input = $http->all();

### Setting An Input

	$http->set('name', 'Bob');

### Forgetting An Input

	$http->forget('name');
