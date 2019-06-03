# Webstorm如何管理嵌套git仓库项目

有时候我们工程代码量比较大的时候，会遇到把子模块拆出去单独一个Git仓库管理的情况。
比如有一个
> 框架工程Framework
。可以独立运行。
Framework下属：
> ModuleA子模块
> ModuleB子模块
> ModuleC子模块

架子工程和子模块有各自管理的Git仓库。

我们运行整个项目的时候，需要分别clone架子工程Framework，以及ModuleA、ModuleB、ModuleC到Framework的指定子目录中。

这时候我们打开webstorm的Version Control面板就会混乱不堪。

[!
