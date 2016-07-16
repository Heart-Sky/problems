2016.7.16 By HeartSky

&nbsp;&nbsp;是在搜apache服务器更改根目录到Windows盘下出现403问题的时候解决的，也明白了为什么屏幕壁纸(在Windows盘下)为什么一重启就恢复成默认，就是因为NTFS分区(我的windows盘是NTFS文件系统)没有开机自动挂载
&nbsp;&nbsp;下面是解决方案
### 0x01
安装ntfs-config，下面是官方介绍，可以看出是`写入权限`，而不是执行权限，很多中文网站上写的都是修改可执行权限，大多还是抄的，简直害人

        This program allow you to easily configure all of your NTFS devices to allow write support via a friendly gui. For that use, it will configure them to use the open source ntfs-3g driver.
``` shell
sudo apt-get install ntfs-3g        # Ubuntu自带
sudo apt-get install ntfs-config    # 图形界面的权限修改配置程序
```
### 0x02
安装成功后启动ntfs-config
``` shell
sudo ntfs-config
```

在弹出的图形化界面中，勾选要获得写入权限的盘，并打勾`启用外部设备写支持`和`启用内部设备写支持`，最后点击关闭就修改成功了
### 0x03
自动挂载好像还需要其他设置，但我给了权限后就自动挂载了，可能是我之前弄过，就差一个权限了吧，等以后重装Ubuntu的时候再来完善吧
