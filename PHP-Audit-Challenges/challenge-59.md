# Challenge 
```php 
 <?php
if (isset($_GET['src']))
    highlight_file(__FILE__) and die();
if (isset($_GET['md5']))
{
    $md5=$_GET['md5'];
    if ($md5==md5($md5))
        echo "Wonderbubulous! Flag is ".require __DIR__."/flag.php";
    else
        echo "Nah... '",htmlspecialchars($md5),"' not the same as ",md5($md5);
}


?>
<p>Find a string that has a MD5 digest equal to itself!</p>
<form>
    <label>Answer: </label>
    <input type='text' name='md5' />
    <input type='submit' />
</form>

<a href='?src'>Source Code</a> 
```

# Solution

```
?md5=0e215962017
```

# Refference 

+ [Hack Dat Kiwi CTF - 2017 md5 game 1](https://ctftime.org/writeup/7784)

