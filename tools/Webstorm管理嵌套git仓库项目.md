# Webstorm如何管理嵌套git仓库项目

有时候我们工程代码量比较大的时候，会遇到把子模块拆出去单独一个Git仓库管理的情况。
比如有一个

> 框架工程Framework

可以独立运行。

Framework下属：

> ModuleA子模块
> ModuleB子模块
> ModuleC子模块

架子工程和子模块有各自管理的Git仓库。

我们运行整个项目的时候，需要分别clone架子工程Framework，以及ModuleA、ModuleB、ModuleC到Framework的指定子目录中。

这时候我们打开webstorm的Version Control面板就会混乱不堪。

![moti_repo.png](https://github.com/Luomusha/blog/blob/master/assets/moti_repo.png)

通常情况下，我们按照各个人员的分工，通常只会对应某一个工程。比如开发人员小朱，在日常开发中只会修改提交ModuleA子模块。
这样其他仓库的改动不需要了解，也不需要追踪。

所以我们可以如下改动：


![resp_setting.png](https://github.com/Luomusha/blog/blob/master/assets/resp_setting.png)

在Webstorm的Version Control界面用‘-’按钮移除追踪的git仓库。
这一步是可以改回来的。不用担心，因为子工程Git仓库一直都存在，只是Webstorm中忽略掉而已。

同过这样设置切换Git仓库，追踪的文件也会随之切换。


> 其实前段工程模块化应该用npm/yarn，通过package.json管理。

