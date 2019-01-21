# linux中的账户体系
在我最常用的debian/ubuntu中，新装的系统会默认内置一些账户。
查看方法：

```bash
cat /etc/passwd
```

会显示如下内容
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
... ...
```
注意其中的www-data账户，就是系统建议的web服务器使用的账户。
注意其中每个账户后面都跟着一堆冒号“：”，分割着一堆参数。
别慌，我们逐个看看他们是什么，代表什么意思，有什么作用。
举例来说；

```
www-data:x:33:33:www-data:/var/www:/bin/bash
```

* www-data  代表用户名
* x         代表密码
* 33        代表用户
* 33        代表用户组
* www-data  代表备注说明/描述
* /var/www  代表用户所在目录
* /bin/bash 代表默认shell

# 启用账户
我们在装完系统后，需要手动启用这个账户，才能用。
首先修改...todo

#  使用

## 生成key

 ```
 ssh-keygen
 ```
## 在gitlab/github中添加sshkey。
略

## 安装ci工具。
