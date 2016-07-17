### 2016.7.16 By HeartSky

记录下Ubuntu下安装LAMP(Linux,Apache,MySQL,PHP)的过程，中间遇到了一个好大的坑 = =

参考链接：
* [如何在Ubuntu 14.04 上安装Linux, Apache, MySQL, PHP (LAMP)组件](http://www.linfuyan.com/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-14-04/)
* [Ubuntu安装Apache2所遇到的问题](http://www.51testing.com/html/38/225738-208454.html)
* [Ubuntu 14.04 安装 Apache](http://cnbin.github.io/blog/2015/07/03/ubuntu-14-dot-04-an-zhuang-apache/)

### 安装Apache
---
>Apache web 服务器是目前世界上最流行的 web 服务器，是挂载站点的最佳默认选择。

安装很简单，一行命令
``` shell
sudo apt-get install apache2
```
执行完后可以测试下
``` shell
http://127.0.0.1
```
如果出现`It works!`的字样，就代表安装成功了
### 安装MySQL
---
>MySQL is an open-source relational database management system (RDBMS)

安装也很简单
``` shell
sudo apt-get install mysql-server php5-mysql
```
安装时，会让你为MySQL的root账户(类似于操作系统的root账户)设置密码
安装完成后还需要执行一些命令来使MySQL生效
``` shell
sudo mysql_install_db   # 创建用于存储信息的数据库目录结构
```
然后运行安全脚本来消除默认的危险配置
``` shell
sudo mysql_secure_installation
```
之后除了修改密码选择no之后。其他的都默认选yes就好了
### 安装PHP
---
>  PHP用于处理代码以显示动态内容。它可以运行脚本，连接到 MySQL 数据库来获取信息，并传输处理好的内容到web服务器来显示。

包含一些辅助包
``` shell
sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
```
如果一个用户向服务器请求目录， Apache会首先寻找名为index.html的文件。我们如果想要web服务器先寻找index.php文件的话，需要经过下面的修改

``` shell
sudo vi /etc/apache2/mods-enabled/dir.conf
```
将其中的`index.php`放在`index.html`的前面，web服务器就会优先处理index.php文件了

### 注意:Apache修改根目录
---
``` shell
sudo vi /etc/apache2/apache2.conf
```
找到`<Directory /var/www/>`，后面的/var/www/就是Apache的根目录，你可以把它更改为自己想要的目录，然后
``` shell
sudo vi /etc/apache2/sites-available/000-default.conf
```
找到`DocumentRoot /var/www/html`，更改为与上面同样的目录

最后重启Apache2服务
``` shell
sudo /etc/init.d/apache2 restart
```
本来这样就可以了，结果访问localhost显示403，把根目录修改到Ubuntu盘下其他位置，是可以正常访问的，便去谷歌，结果谷歌了一个多小时都没找到有效的解决方案，后来想了下可能是权限的问题，但Windows盘下文件已经777了，实在想不通，再去尝试谷歌`ubuntu apache 根目录 修改到windows盘`，终于在一篇文章中找到了解决方案
``` shell
cd /etc/apache2
sudo vi apache2.conf
```
把
``` shell
User ${APACHE_RUN_USER}
Group ${APACHE_RUN_GROUP} 
```
修改为
``` shell
User (your_user_name)
Group (your_user_group)
```
比如我是
``` shell
User heartsky
Group heartsky
```
暂时不明白为什么这样就可以了，明天再来研究下，然后就去写PHP了。不管怎样，终于解决了，好兴奋

在`/etc/apache2/envvars`中发现有这么一段代码
``` shell
export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data
```
所以我们进行的操作是把Apache的运行用户及所在组从默认的www-data更改为自己的用户名及所在组，至于为什么默认的www-data的时候不能访问windows盘，则不得而知了，或许还是权限问题吧

