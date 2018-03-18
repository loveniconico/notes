# 安装
如果你不使用 Homestead，则需要确保你的服务器符合以下要求：  
PHP >= 7.0.0   
PHP OpenSSL 扩展  
PHP PDO 扩展  
PHP Mbstring 扩展  
PHP Tokenizer 扩展  
PHP XML 扩展   
Laravel 利用 Composer 来管理依赖。所以，在使用 Laravel 之前，请确保你的机器上安装了 Composer。  

**安装步骤:**  
1. `composer global require "laravel/installer"`
2. `laravel new [项目名称]`

## 安装`barryvdh/laravel-ide-helper`
在项目的根目录运行  
`composer require barryvdh/laravel-ide-helper`  
然后在 `config/app.php` 中添加  
`Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,`  
### PHPStorm使用Artisan生成PHPDoc辅助文件
`settings——Tools | Command Line Tool Support` --添加一个新的命令行。  
将项目根目录下的 `artisan` 文件引入  
然后在菜单栏中打开 `Tools | Run Command…`  
运行 `artisan ide-helper:generate` 命令可以生成必要的 PHPDoc信息。

>Laravel IDE Helper在每次改变服务或添加服务、控制器、模型以及视图的时候都要重新运行一下。Laravel IDE Helper的github主页上给出了一些运行建议。例如，在安装或更新Composer依赖之后，运行Laravel IDE Helper。另一种比较简便的方法就是使用PHPStorm软件的`File Watchers`文件监控，这可以自动化地在一些文件修改之后，重新生成Laravel IDE Helper文件，例如`composer.json`文件的修改。
> ```json
>"scripts":{
>    "post-update-cmd": [
>        "Illuminate\\Foundation\\ComposerScripts::postUpdate",
>        "php artisan ide-helper:generate",
>        "php artisan ide-helper:meta",
>        "php artisan optimize"
>    ]
>},
>```
在PHPStorm安装并启用Laravel Plugin插件
