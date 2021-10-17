# Challenge
```php
$url = 'file://localhost/etc/passwd'
$parts = parse_url($url);
if (empty($parts['hosts']) || $parts['host'] != 'localhost'){
    exit('error');
}
readfile($url);
?>
```


# Refference

这里我的理解是，作者让我们绕过if判断 读取 \etc\passwd 的文件
但是这里又没有可控的参数，parse_url 输出又没有 hosts 的键，完全无从下手 @_@

+ [parse_url()](http://phpweb.hostnet.com.br/manual/zh/function.parse-url.php)

