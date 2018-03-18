# 跨域获取cookie
## 跨二级域名
这个简单,只需要在创建cookie时候指定域名就可   
假设域名是:
- oauth2.php123.com
- www.php123.com
```php
setcookie("foo1", "bar1", time() + 3600, "/", "php123.com");
```

## P3P完成cookie跨域
www.a.com/index.php
```php
<?php
header('P3P: CP="CURa ADMa DEVa PSAo PSDo OUR BUS UNI PUR INT DEM STA PRE COM NAV OTC NOI DSP COR"');
setcookie("test", $_GET['id'], time()+3600, "/", ".a.com");  
```
www.b.com/index.php
```php
<script src="http://www.a.com/index.php?id=www.b.com"></script>  
```
运行b.com时就可以设置a.com的cookie