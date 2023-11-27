# 更新pve软件源方法1



PVE 虚拟机主机 更换国内源以及解决无效订阅的问题

1、PVE更换国内源

 注：本文以 pve 7.3.3 为例。

替换前建议先更新下证书，否则可能由于证书不可用导致 https 无法使用，进而无法下载所有软件。

```
apt install apt-transport-https ca-certificates
```
注意：这个步骤出现错误就反复重复运行上面这条命令直到成功，有时候网络不好会失败

首先替换通用软件源， Debian 的软件源配置文件是 /etc/apt/sources.list，备份后将其中内容修改为以下即可。

```
cd /etc/apt/
```





阿里云软件源
https://developer.aliyun.com/mirror/ubuntu?spm=a2c6h.13651102.0.0.3e221b113SE1l6
阿里云软件源
ubuntu 18.04(bionic) 配置如下

```
deb https://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

# deb https://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```


或者用
清华大学debian软件源
```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free

deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free

deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free
```












 ctrl+x 再按Y，回车，就可以完成。

之后替换 pve 软件源，pve 镜像默认的 pve 软件源配置文件是 /etc/apt/sources.list.d/pve-enterprise.list ，

```
cd /etc/apt/sources.list.d/
```




备份后将其中内容替换为以下即可：(修改步骤同前面。)
```
deb https://mirrors.tuna.tsinghua.edu.cn/proxmox/debian bullseye pve-no-subscription
```


# 更新pve软件源方法2

https://huaweicloud.csdn.net/6356198bd3efff3090b5a2a5.html

因PVE7.0更换了Debian11作为内核，软件源管理方式也发生了变更，故原软件源配置方法已失效。

默认是企业订阅版，如果不做修改，在使用 pveceph init 进行 ceph 初始化安装的时候会将整个环境破坏，切记！

登陆各节点Shell控制台  
【重要】将/etc/apt/sources.list.d/pve-enterprise.list 文件内的唯一一条记录注释掉：

```
echo "#deb https://enterprise.proxmox.com/debian/pve bullseye pve-enterprise" > /etc/apt/sources.list.d/pve-enterprise.list
```




Proxmox软件源更换  
中科大源（二选一）：

```
wget https://mirrors.ustc.edu.cn/proxmox/debian/proxmox-release-bullseye.gpg -O /etc/apt/trusted.gpg.d/proxmox-release-bullseye.gpg
echo "deb https://mirrors.ustc.edu.cn/proxmox/debian/pve bullseye pve-no-subscription" > /etc/apt/sources.list.d/pve-no-subscription.list     #中科大源
echo "deb https://mirrors.ustc.edu.cn/proxmox/debian/ceph-pacific bullseye main" > /etc/apt/sources.list.d/ceph.list     #中科大源
sed -i.bak "s#http://download.proxmox.com/debian#https://mirrors.ustc.edu.cn/proxmox/debian#g" /usr/share/perl5/PVE/CLI/pveceph.pm     #中科大源
apt update && apt dist-upgrade     #更新软件，可不执行
```


Proxmox中文社区源（二选一）：

```
wget http://download.proxmox.wiki/debian/proxmox-release-bullseye.gpg -O /etc/apt/trusted.gpg.d/proxmox-release-bullseye.gpg
echo "deb http://download.proxmox.wiki/debian/pve bullseye pve-no-subscription" > /etc/apt/sources.list.d/pve-no-subscription.list     #Proxmox中文社区源
echo "deb https://download.proxmox.wiki/debian/ceph-pacific bullseye main" > /etc/apt/sources.list.d/ceph.list     #Proxmox中文社区源
sed -i.bak "s#http://download.proxmox.com/debian#https://download.proxmox.wiki/debian#g" /usr/share/perl5/PVE/CLI/pveceph.pm     #Proxmox中文社区源
apt update && apt dist-upgrade     #更新软件，可不执行
```


Debian系统源更换  
阿里Debian源（二选一）：
```
sed -i.bak "s#ftp.debian.org/debian#mirrors.aliyun.com/debian#g" /etc/apt/sources.list     #阿里Debian源
sed -i "s#security.debian.org#mirrors.aliyun.com/debian-security#g" /etc/apt/sources.list     #阿里Debian源
apt update && apt dist-upgrade     #更新软件，可不执行
```


163-Debian源（二选一）：
```
sed -i.bak "s#ftp.debian.org/debian#mirrors.163.com/debian#g" /etc/apt/sources.list     #163Debian源
sed -i "s#security.debian.org#mirrors.163.com/debian-security#g" /etc/apt/sources.list     #163Debian源
apt update && apt dist-upgrade     #更新软件，可不执行
```

删除订阅弹窗
```
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
# 执行完成后，浏览器Ctrl+F5强制刷新缓存
```

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