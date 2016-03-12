# 2016.3.11 by HeartSky
### 0x00
说是教程，实则是安装及配置时遇到的一些问题
### 0x01
去官方下载软件时，在chrome下没下完就提示下完了，打开后不能运行，火狐下也是，不过火狐提示的是下载失败，不知道为什么，然后失败后就一直点继续下载，最后成功了
### 0x02
安装后打开，右下角出来图标，但无法对其操作，多次尝试后在安装文件夹里找到了`install-english.txt`，找到原因，在安装前要下载各种版本的`Visual C++`，之后成功运行
### 0x03
配置php，打开bin->php->php.ini
    
short_open_tag = Off（是否允许使用 PHP代码开始标志的缩写形式（<? ?>））；
教程说改为On，个人觉得不用，推荐使用php的标准形式`<?php ?>`
    
memory_limit = 128M（最大使用内存的大小）；
upload_max_filesize = 2M（上传附件的最大值），
以上根据实际需要修改

<del>暂时写到这，使用过程中有新发现再来完善 = =<\del>

### 0x04
修改www目录，后来想了下，放在软件目录里不太保险，万一哪天手贱把软件卸了，忘记网页文件还在里面。
    
打开scripts->config.inc.php,把`$wwwDir =$c_installDir.'/www';`改成自己想要的目录,我是直接改成了`$wwwDir = 'E:/code/website/';`(后来的时候出了问题，不知道和删了$c_installDir.有没有关系= =)，有一点要注意，windows下表示路径的\要改为/
    
还没完，再打开httpd.conf，相应改为`DocumentRoot "your_path"`和`<Directory "your_path">`

按理说到现在就可以了，不知道为什么目录还是没更改，重启服务也不行，后来重启电脑结果莫名其妙的可以了
    
暂时告一段落，开始撸php ：)
