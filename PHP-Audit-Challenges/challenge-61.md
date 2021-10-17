# Challenge 
```php 
 <?php
    $sandbox = "sandbox/" . md5("orange" . $_SERVER["REMOTE_ADDR"]);
    @mkdir($sandbox);
    @chdir($sandbox);

    $data = shell_exec("GET " . escapeshellarg($_GET["url"]));
    $info = pathinfo($_GET["filename"]);
    $dir  = basename($info["dirname"]);
    @mkdir($dir);
    @chdir($dir);
    @file_put_contents(basename($info["basename"]), $data);
    highlight_file(__FILE__);

```

# Solution

查看根目录

```
?url= /&filename=666.txt
```

# Refference

+ [hitcon ctf 2017  SSRFme?](https://mayi077.gitee.io/2020/03/25/HITCON-2017-SSRFme/)

