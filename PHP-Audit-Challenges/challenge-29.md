# Challenge 
```php 
<?php
 include('config.php');
 session_start();

 if($_SESSION['time'] && time() - $_SESSION['time'] > 60){
    session_destroy();
    die('timeout');
 } else {
    $_SESSION['time'] = time();
 }

 echo rand();
 if(isset($_GET['go'])){
    $_SESSION['rand'] = array();
    $i = 5;
    $d = '';
    while($i--){
        $r = (string)rand();
        $_SESSION['rand'][] = $r;
        $d .= $r;
    }
    echo md5($d);
 }else if(isset($_GET['check'])){
    if($_GET['ckeck'] === $_SESSION['rand']){
        echo $flag;
    } else {
        echo 'die';
        session_destroy();
    }
 } else {
    show_source(__FILE__);
 }
?>
```

# Solution

```python
#encoding:utf-8
import requests
while True:
    r = requests.session()
    l = []
    # 获取50个随机rand值并存入list
    for i in range(50):
        response = r.get('http://localhost/php_challenge/29.php')
        l.append(int(response.content[:response.content.find('<')]))
    #将$_SESSION['rand']这个数组写满5个随机数
    response = r.get('http://localhost/php_challenge/29.php?go')
    #获取将MD5之前的rand随机数存到list
    l.append(int(response.content[:-32]))
    url = 'http://localhost/php_challenge/29.php?'
    for i in range(5):
        end = len(l)
        #由随机数生成算法预测下一个随机数
        randNUM = (l[end-3]+l[end-31]) % 2147483648
        l.append(randNUM)#将新生成的也加入到列表里
        #构造url 传入数组5个预测rand随机数
        url += 'check[]={}&'.format(randNUM)
    response = r.get(url)#GET请求url 同时传入参数
    #如果输出不是 die 大功告成
    if 'die' not in response.content:
        print response.content
        break
```

# Refference

+ [2016 0ctf Rand_2](http://drops.xmd5.com/static/drops/tips-13791.html)

+ [2016 0ctf Rand_2](https://www.virzz.com/2016/03/14/some_web_writeup_for_0ctf_2016.html)

