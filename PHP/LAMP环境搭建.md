# 1. 要先有个 linux 系统，我选择了 Ubuntu
 如何安装 Ubuntu 我就不赘述了  
 我使用的是 windows 的子系统 `bash` ，Ubuntu 16.04.2 LTS   
 有了 Ubuntu 我们还要有个 Ubuntu 账户，当然服务器要联网  
 不同的系统配置会稍有不同  
 LNMP的搭建也是大同小异

# 2. 用 `Xshell` 连接服务器，并且操作服务器
- 因为是用 `ssh` 连接的所有要在服务器上安装 `openssh-server` （一般是默认安装的，安装命令`sudo apt-get install openssh-server`  
- 然后启动 `openssh-server` 使用命令 `/etc/init.d/ssh start[启动]`.`restart[重启]`.`stop[停止]`  
- 使用 `ps -e | grep ssh` 查看是否启动，`ssh-agent` 表示未启动，`xxx     sshd` 表示已启动   
- 然后设置下 Ubuntu 的 `ssh` 的配置文件，默认情况下是强制要求使用 `密钥[公钥/私钥]` 连接，要使用密码连接就要修改 `ssh` 的配置文件。   
- 修改 `ssh` 的配置文件 `sudo vi /etc/ssh/sshd_config`，直接编辑，将字段 `PasswordAuthentication no` 改为 `PasswordAuthentication yes`，然后保存，这样就可以连接了   
- 打开 `Xshell` ,点击新建，名称你高兴就好，协议为 `SSH` ，主机地址（`ifconfig` 命令可以查看），端口默认为 `22`  点击确定，然后输入用户名和用户密码，再点击连接就 ok 了

# 3. 安装Apache2，PHP7,MySQL5
## 3.1. 安装Apache2
- 安装：`sudo apt-get install apache2`   
- 启动 apache 服务器：`/etc/init.d/apache2 start`   
- 在浏览器上的地址栏填写服务器的 IP 地址，当页面有响应且是 apache 的解释就说明安装成功了   
    > ### apache常用命令  
    > 配置文件是：`/etc/apache2/apache2.conf`  
    > 启动：`sudo service apache2 start`  
    > 停止：`sudo service apache2 stop`  
    > 重新启动：`sudo service apache2 restart`  
    > www目录为：`/var/www/html` 需要修改权限 `sudo chmod 777 /var/www/html` 否则无法添加和更新内容  

## 3.2. 安装PHP7
- 安装：`sudo apt-get install php7.0`   
- 安装 apache 的 PHP 模块：`sudo apt-get install libapache2-mod-php7.0`   
- 重启 apache 服务：`sudo service apache2 restart`   
- 检查是否加载了模块：`cat /etc/apache2/mods-enabled/php7.0.load`   
    为 `LoadModule php7_module /usr/lib/apache2/modules/libphp7.0.so` 是成功加载模块

## 3.3. 安装MySQL
- 安装：`sudo apt-get install mysql-server` 会提示要求输入root账户的密码  
- 安装 PHP 的 MySQL 模块：`sudo apt-get install  php7.0-mysql`   
- 检查是否加载了模块：`cat /etc/php/7.0/mods-available/mysqli.ini`
    为 `extension=mysqli.so` 是成功加载模块
- 允许外部地址远程访问 MySQL 
    修改 MySQL 的配置文件 `/etc/mysql/mysql.conf.d/mysqld.cnf`   
    注释 `bind-address           = 127.0.0.1`   

## 3.4. 创建 PHP 服务器探针
在 `/var/www/html` 目录下新建文件 `index.php` 
添加文件内容
```php
<?php
  echo mysqli_connect('127.0.0.1','root','******') ? '连接成功' : '连接失败';

  phpinfo();
```
然后我们在浏览器的地址栏上输入服务器的 IP 地址，有 `连接成功` 的字样和 phpinfo 的信息 就说明安装Apache2，PHP7,MySQL5，与他们之间的连接没问题，到此 LAMP 服务器环境搭建完毕。

# 4.扩展
## 4.1. 一行命令安装Apache2，PHP7,MySQL5
```
sudo apt-get install apache2 php7.0 libapache2-mod-php7.0 mysql-server php7.0-mysql
```
## 4.2. 一行命令安装 LAMP
```
sudo tasksel install lamp-server
```
## 4.3. 使用 SSH（SFTP）管理文件
> 我用的是 `FlashFXP` 
菜单栏 -> 站点 -> 站点管理器（快捷键是 <kbd>F4</kbd>）  
连接类型为 `SFTP over SSH`
然后是用户名和用户密码
