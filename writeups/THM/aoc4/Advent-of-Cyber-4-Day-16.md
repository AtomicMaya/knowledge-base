# Advent of Cyber 4 - Day 16

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the value of Flag1?

```php
include "connection.php";

	$query="select * from users where id=".intval($_GET['id']);
	$elves_rs=mysqli_query($db,$query);

	if(!$elves_rs)
	{
		echo "<font color=red size=10>Error: Invalid SQL Query</font>";
		die($query);
	}

	// Get the first result. There should be a single elf here.
	$elf=mysqli_fetch_assoc($elves_rs);

	//Now get the toys associated to this elf
	$query="select * from toys where creator_id=".intval($_GET['id']);
	$toys_rs=mysqli_query($db,$query);

	if(!$toys_rs)
	{
		echo "<font color=red size=10>Error: Invalid SQL Query</font>";
		die($query);
	}
```

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day16/1.png?raw=true)

Answer: `THM{McCode, Elf McCode}`

### Question 2

> What is the value of Flag2?

```php
$query="select * from toys where name like ? or description like ?";
$stmt = mysqli_prepare($db, $query);
$q = "%".$_GET['q']."%";
mysqli_stmt_bind_param($stmt, 'ss', $q, $q);
mysqli_stmt_execute($stmt);
$toys_rs=mysqli_stmt_get_result($stmt);

if(!$toys_rs)
{
	echo "<font color=red size=10>Error: Invalid SQL Query</font>";
	die($query);
}
```

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day16/2.png?raw=true)

Answer: `THM{KodeNRoll}`

### Question 3

> What is the value of Flag3?

```php
		include "connection.php";

	$query="select * from toys where id=".intval($_GET['id']);
	$toys_rs=mysqli_query($db,$query);

	if(!$toys_rs)
	{
		echo "<font color=red size=10>Error: Invalid SQL Query</font>";
		die($query);
	}

	// Get the first result. There should be a single elf here.
	$toy=mysqli_fetch_assoc($toys_rs);

	//query info on the creator elf
	$query="select * from users where id=".intval($toy['creator_id']);
	$elves_rs=mysqli_query($db,$query);

	if(!$elves_rs)
	{
		echo "<font color=red size=10>Error: Invalid SQL Query</font>";
		die($query);
	}

	// Get the first result. There should be a single elf here.
	$elf=mysqli_fetch_assoc($elves_rs);
	
	//query info on planned deliveries
	$query="select * from kids where assigned_toy_id=".intval($_GET['id']);
	$kids_rs=mysqli_query($db,$query);

	if(!$kids_rs)
	{
		echo "<font color=red size=10>Error: Invalid SQL Query</font>";
		die($query);
	}
```

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day16/3.png?raw=true)

Answer: `THM{Are we secure yet?}`

### Question 4

> What is the value of Flag4?

```php
if(isset($_POST['username']) && isset($_POST['password'])){
	$username=$_POST['username'];
	$password=$_POST['password'];
	$query="select * from users where username=? and password=?";
	$stmt = mysqli_prepare($db, $query);
	mysqli_stmt_bind_param($stmt, 'ss', $username, $password);
	mysqli_stmt_execute($stmt);
	$users_rs=mysqli_stmt_get_result($stmt);
	
	if(mysqli_num_rows($users_rs)>0)
	{
		$_SESSION['username']=$username;
		echo "<script>window.location='admin.php';</script>";
	}
	else
	{
		$message="Incorrect username/password found!";
		echo "<script type='text/javascript'>alert('$message');</script>";
	}
}
```

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day16/4.png?raw=true)

Answer: `THM{SQLi_who???}`
