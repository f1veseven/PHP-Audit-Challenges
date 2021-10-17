# Challenge
```php 
<h1>hello ctfer!<h1><!--<?php
error_reporting(0);
$flag = "xxxxxxxx";
$secret = "xxxxxxxxxxxxxxxxxxxxxxxxx"; // This secret is 15 characters long for security!
$username = $_POST["username"];
$password = $_POST["password"];
if (!empty($_COOKIE["getmein"])) {
    if (urldecode($username) === "admin" && urldecode($password) != "admin") {
        if ($_COOKIE["getmein"] == md5($secret . urldecode($username . $password))) {
            echo "Congratulations! You are a registered user.\n";
            die ("The flag is ". $flag);
        }
        else {
            die ("Your cookies don't match up! STOP HACKING THIS SITE.");
        }
    }
    else {
        die ("You are not an admin! LEAVE.");
    }
}
setcookie("sample-hash", md5($secret . urldecode("admin" . "admin")), time() + (60 * 60 * 24 * 7));
echo "<h1>hello ctfer!<h1>";
-->
```

# Solution

此题主要考察hash长度扩展，利用hashpump
hashdump工具的使用参考一下链接

# Refference

+ [Web: HASH](https://www.dazhuanlan.com/oluoz2/topics/1422998)

https://blog.csdn.net/dyw_666666/article/details/89448729