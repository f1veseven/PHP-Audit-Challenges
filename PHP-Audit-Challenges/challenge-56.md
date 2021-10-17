# Challenge 
```php 
<?php

$db  = mysqli_connect('localhost','web_brave','','web_brave');

$id  = @$_GET['id'];
$key = $db->real_escape_string(@$_GET['key']);

if(preg_match('/\s|[\(\)\'"\/\\=&\|1-9]|#|\/\*|into|file|case|group|order|having|limit|and|or|not|null|union|select|from|where|--/i', $id))
    die('Attack Detected. Try harder: '. $_SERVER['REMOTE_ADDR']); // attack detected

$query = "SELECT `id`,`name`,`key` FROM `users` WHERE `id` = $id AND `key` = '".$key."'";
$q = $db->query($query);

if($q->num_rows) {
    echo '<h3>Users:</h3><ul>';
    while($row = $q->fetch_array()) {
        echo '<li>'.$row['name'].'</li>';
    }

    echo '</ul>';
} else {    
    die('<h3>Nop.</h3>');
}
```
# Solution
```
/index.php?id=id;%00
```

```
sql语句中 `id`=$id 在mysql识别是可以直接用 `id`=id 使 where条件相等
```



# Refference 

+ [D-CTF 2017 quals:Are you brave enough?](https://titanwolf.org/Network/Articles/Article?AID=6d2c8d9b-2e7d-44b0-92cd-b8c51f059809) 

