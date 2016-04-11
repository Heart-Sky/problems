# 2016.4.11 by HeartSky
### 0x00
昨天安装sqli-labs练习平台时，把wamp弄崩了，无法访问服务器，只能重装，今天成功解决，那就分享一下过程
### 0x01
因为这个平台用的是mysql连接方式，而php5以上的版本默认不支持mysql，所以首先让它支持mysql
    
打开php.ini，添加一行`extension=php_mysql.dll`，这表示激活了mysql_mysql动态连接库，要想php能和mysql通过这种方式进行交互，还需要把`libmysql.dll`（可从网上下载）复制到system32目录下，然后重启wamp服务就可以了
### 0x02
之后到https://github.com/Audi-1/sqli-labs下载练习平台的源码，放到网站根目录下，比如我是`E:\code\website\sqli-labs-master`。修改db-creds.inc 文件，添加你的 mysql 账户和密码，然后打开index.html，点击`Setup/reset Database for labs`，安装成功了就可以 愉 ♂ 快 ♀ 的开始注入了
