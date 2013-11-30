
Connecting to MySQL using PHP can be a tad tricky as MySQL is configured on Feral to only allow connections via socket.

To make it work use the following line to connect:

~~~
$db = MySQLi_connect("localhost","root",'password', '', 0, '/path/to/your/mysql/socket');
~~~

or

~~~
mysql_connect("localhost:SOCKETNAME", "root", "PASSWORD") or die(mysql_error()); mysql_select_db("DATABASE_NAME") or die(mysql_error());
~~~

It's one full line and the variables are in uppercase:

**SOCKETNAME**: found in your **my.conf** file

~~~
~/private/mysql/my.conf
~~~

**PASSWORD**: your MySQL password

**DATABASE_NAME**: the database you created in mysql

With PDO, it's special !

In php many PDo connections will use a similar layout:

~~~
<?php

$dsn = 'mysql:dbname=testdb;host=localhost';
$user = 'dbuser';
$password = 'dbpass';

try {
$dbh = new PDO($dsn, $user, $password);
} catch (PDOException $e) {
echo 'Connexion échouée : ' . $e->getMessage();
}

?>
~~~

On feralhosting PDO can use a socket, but you cannot have `host` and `unix_socket=` simultaneously for a connection.
The default Feral set up is for local connections only. So you would need to replace `host` with `unix_socket=`

In this example the socket has been hard coded. If the php app provides a variable for the hostame, for use with a web based installer for example, you could use that.

example :

~~~
<?php

$dsn = 'mysql:dbname=testdb;unix_socket=/media/path/to/mysql/socket';
$user = 'dbuser';
$password = 'dbpass';

try {
$dbh = new PDO($dsn, $user, $password);
} catch (PDOException $e) {
echo 'Connexion échouée : ' . $e->getMessage();
}

?>
~~~

