

[制作pve安装的镜像](制作pve安装的镜像.md)


[安装pve](安装pve.md)


# 安装pve桌面版

安装pve的kde桌面的教程
https://www.bilibili.com/video/av892036573/





# [pve更新软件源](pve更新软件源.md)


# 安装kde桌面

KDE Plasma桌面环境，是新一代 Linux 桌面环境，有着轻量化兼容性广的特点，对应PVE虚拟机来说可以扩展一个图形界面的linux操作系统，非常有可玩性

前面的步骤做完
后更新下，速度很快：

一、更新PVE软件源

```
apt-get update
```
注意：这个步骤出现错误就反复重复运行上面这条命令直到成功，有时候网络不好会失败
2
```
apt-get upgrade
```
注意：这个步骤出现错误就反复重复运行上面这条命令直到成功，有时候网络不好会失败

如果更新不了就先解决
[PVE网络不好或终端连不上linux网络不好](PVE网络不好或终端连不上linux网络不好.md)
的问题

## 二、一条命令进行安装

默认情况下，KDE Plasma 在 [Debian 11](https://www.yundongfang.com/Yuntag/debian-11) 基础存储库中可用。现在运行以下命令在 Debian 系统上[安装 KDE Plasma](https://www.yundongfang.com/Yuntag/%e5%ae%89%e8%a3%85-kde-plasma) 桌面环境：

```
apt-get install task-kde-desktop
```
注意：这个步骤出现错误就反复重复运行上面这条命令直到成功，有时候网络不好会失败
100%成功后

##### 硬件重启PVE主机
看启动界面有没有变化了
```
reboot
```

## 三、设置用户名和密码


创建admin用户
```
useradd -m admin
```
例如

```
useradd -m a
```

设置admin用户密码

```
passwd admin
```
设置admin用户a的桌面登录用户密码
例如
```
passwd a
```
例如
```
123456
```


设好以后pve右上角重启按钮重启
就会出现桌面账号的框了

桌面账号
a
桌面密码
123456

更改语言为中文



# 桌面账号
桌面账号
a
桌面密码
123456




更改语言为中文
system settings》personalization》regional settings》language》add languages》加入简体中文》把简体中文排序调整到上面第一位》apply保存

登出系统再登入
开始菜单》leave》settion》log out》OK

百度搜索中下载和安装firefox的linux版本的浏览器
下载以后会自动安装


# pve操作界面

https://192.168.0.90:8006


# pve账号
pve账号https
root
pve密码
123456



[PVE安装zerotier实现内网穿透](PVE安装zerotier实现内网穿透.md)