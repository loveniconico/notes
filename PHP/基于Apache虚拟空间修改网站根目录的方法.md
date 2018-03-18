# 基于Apache虚拟空间修改网站根目录的方法

对于是使用虚拟空间搭建WEB应用的用户来说,一些流行框架例如: `laravel` 其入口文件在项目目录下的 `public` 中,但是虚拟空间又无法更改网站的根目录,于是就有了下面的解决方法

在网站根目录建立 `.htaccess` 文件，里面代码为， 

```.htaccess
<IfModule mod_rewrite.c> 
    RewriteEngine on 
    RewriteCond %{REQUEST_URI} !^public 
    RewriteRule ^(.*)$ %ROOT%/$1 [L] 
</IfModule> 
```

`%ROOT%` 为入口文件相对于网站根目录的相对路径