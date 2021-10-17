# Challenge 
```php 
<?php
    show_source(__FILE__);
    $pass = @$_GET['pass'];
    $a = "syclover";

    strlen($pass) > 15 ? die("Don't Hack me!") : "";

    if(!is_numeric($pass) || preg_match('/0(x)?|-|\+|\s|^(\.|\d).*$/i',$pass)){
        die('error');
    }

    if($pass == 1 &&  $a[$pass] === "s"){
        $file = isset($_GET['f']) ? $_GET['f'].'.php' : 'index.php';
        @include $file;
    }
?>
```

# Solutioin

环境问题，未复现成功

# Refference
+ [SCTF2016:Pentest-sycshell](http://virink.blogspot.jp/2016/05/sctf2016.html)
+ https://docs.ioin.in/writeup/www.isecer.com/_ctf_sctf2016_painful_penetrating_way_html/index.html