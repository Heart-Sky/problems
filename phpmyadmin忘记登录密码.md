# 2016.4.1 by HeartSky
### 0x00
前天把密码修改了，但作死的选择了自带的`native mysql authentication`加密方式（具体是什么加密方式先不管），当时不知道是干啥的啊，于是密码成了加密后的一个字符串，再登录时就呵呵了
### 0x01
尝试md5加密和base64加密形成的字符串都无果后，果断去找谷歌了
        
刚开始试了几种方法都未能解决，差点想重新装wamp了，还是理性了下来，转手搜英文
### 0x02
谷歌`phpmyadmin forgot pass windows`，果然还是英文资料比较靠谱，参考[链接](http://www.jovicailic.org/2012/04/reset-forgotten-mysql-root-password-under-windows/)，写的实在赞，自己去看吧。其中有个坑，在MySQL5.7中,password字段在mysql.user表字段 中被去除了, 新的字段名字是'authentication_string'，其他的很完美了，自己跟着弄就好了

### 总结
>某大大：不懂就问谷狗，找不到问题的答案就再用英文描述一遍问题，再问谷狗
