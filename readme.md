# MySQLi Database Class

## Overview
Wrapper for a PHP MySQL class, which utilizes MySQLi and prepared statements.

1. Initialisation
1. Insert Query
2. Select Query
3. Select Query
4. Update Query
5. Delete Query
6. Generic Query Method
7. Row Query Method
8. Where Method



### 1. Initialisation

to utilize this class, first import Mysqldbi.php into your project, and require it.


	require_once('Mysqlidb.php');


After that, create a new instance of the class.

	$db = new Mysqlidb('host', 'username', 'password', 'databaseName');


Next, prepare your data, and call the necessary methods. 

<h3>2. Insert Query </h3>


	$insertData = array(
		'title' => 'Inserted title',
		'body' => 'Inserted body'
	);
	
	if ( $db->insert('posts', $insertData) ) echo 'success!';



<h3>3. Select Query </h3>


	$results = $db->get('tableName', 'numberOfRows-optional');
	print_r($results); // contains array of returned rows


<h3>4. Update Query </h3>

	$updateData = array(
		'fieldOne' => 'fieldValue',
		'fieldTwo' => 'fieldValue'
	);
	$db->where('id', int);
	$results = $db->update('tableName', $updateData);


<h3>5. Delete Query </h3>

	$db->where('id', int);
	if ( $db->delete('posts') ) echo 'successfully deleted'; 

<h3>6. Generic Query Method </h3>

	$results = $db->query('SELECT * from posts');
	print_r($results); // contains array of returned rows

<h3>7. Raw Query Method </h3>


	$params = array(3, 'My Title');
	$resutls = $db->rawQuery("SELECT id, title, body FROM posts WHERE id = ? 	AND tile = ?", $params);
	print_r($results); // contains array of returned rows

	// will handle any SQL query

	$params = array(10, 1, 10, 11, 2, 10);
	$resutls = $db->rawQuery("
	(SELECT a FROM t1 WHERE a = ? AND B = ? ORDER BY a LIMIT ?)
	UNION
	(SELECT a FROM t2 WHERE a = ? AND B = ? ORDER BY a LIMIT ?)
	", $params);
	print_r($results); // contains array of returned rows




<h3>8. Where Method </h3>
This method allows you to specify the parameters of the query.

	$db->where('id', int);
	$db->where('title', string);
	$results = $db->get('tableName');
	print_r($results); // contains array of returned rows

Optionally you can use method chaining to call where multiple times without referancing your object over an over:

	$results = $db
		->where('id', 1)
		->where('title', 'MyTitle')
		->get('tableName');


