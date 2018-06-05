# 安装步骤
## 在hyper-v中新建设备、硬盘、网络连接
## 安装中可能遇到的错误：

### 1. 电脑安装（相对于虚拟机而言）
我的电脑是nvidia和intel混合双显卡，在安装时候遇到了以下错误

```bash
Started TLP system startup/shutdown
A start job is running for livemedia mhwd scripe(xx s/no limit)
```

然后就一直卡住。中文资料比较少，费了很大力气和时间成本终于解决。可以确定的原因是混显卡造成的。
可能的原因有两个

假如你是用真实的电脑安装（相对于虚拟机而言），
需要在安装的时候，进入安装界面后选择driver=free上，按键盘E键，进入编辑模式，然后手动将free改成intel。
然后按F10保存后boot启动。

### 2. hyper-v

上述方法在我用电脑时候好用，我这里用的是hyper-v虚拟机无效。进去之后还是不现实图形化界面


![st.png](https://github.com/Luomusha/blog/blob/master/assets/st.png)


在进入之后不显示界面

按住Ctrl+alt+F3进入命令行，输入以下命令(可能需要家sudo)：

```
Graphical programs can easily be run via Xorg via the xf86-video-fbdev package. Simply install it and the window manager or desktop environment you wish to use, and you should be able to start X without issue.
```

所以hyper-v不是全虚拟化，不能直接安装显卡驱动，而是用这个xf86-video-fbdev包做驱动

```bash
pacman -Syy
pacman -R nvidia nvidia-libgl lib32-nvidia-libgl
pacman -S xf86-video-fbdev

startx
```

上面的命令的意思是：
1.包管理器pacman同步（更新）
2.卸载nvidia驱动
3.安装hyper-v驱动
4.开启图形化桌面

![done.png](https://github.com/Luomusha/blog/blob/master/assets/done.png)

参考链接
https://bbs.archlinux.org/viewtopic.php?id=211846
https://wiki.archlinux.org/index.php/Hyper-V



# 如果你没有安装成功，那么一定是你被墙了
# 如果你更新报错，那么一定是你被墙了
# 如果你软件build失败，那么一定是你被墙了
