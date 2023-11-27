https://www.youtube.com/watch?v=X6kaDbZOm9Q

proxmax.com
PVE虚拟环境macOS系统基本应用以及优化（虚拟机装黑果果02）


https://www.youtube.com/watch?v=S0V9jPUB4JM


https://www.youtube.com/watch?v=LQ1BPsLwPF8
【司波图】PVE下针对macOS的显卡直通设置（虚拟机装黑果果03_完结）
https://www.youtube.com/watch?v=LQ1BPsLwPF8



https://www.bilibili.com/video/BV1uq4y1g7ui/

[pve安装一个ubungtu系统](pve安装一个ubungtu系统)


# pve里做一个ubungtu的类似ghost的引导盘


回到PVE网页页面

pve》local（pve)》CT模板

选一个ubungtu的
下载如果网速不好卡住了
里面会提示它的下载地址的

windows端打开网页手动下载了上传到pve服务器里去

例如
http://download.proxmox.com/images/system/ubuntu-18.04-standard_18.04.1-1_amd64.tar.gz

pve》local（pve)》CT模板》上传

创建CT


```
----------------------
常规
----------------------
节点：pve
CT ID:100
主机名：随便写例如ubungtu18.04
确认密码：
无特权的容器：☑
嵌套：☑

加载SSH密钥文件


资源池：
密码：123456
确认密码：123456
SSH公钥：
----------------------
模板
----------------------
存储：local
模板：ubuntu-18.04-standard_18.04.1-1_amd64.tar.gz


----------------------
磁盘
----------------------
存储：local-lvm
磁盘大小(GiB):16


----------------------
CPU
----------------------
核心：4

----------------------
内存
----------------------
内存(MiB):1024
Swap (MiB):1024


----------------------
网络
----------------------
IPV4  DHCP


----------------------
DNS
----------------------
----------------------
确认
----------------------
```


点击左边创建好的100 ubungtu18.04容器
登录
root
123456

这里可将这个服务器连上finalshell操作



# A1:在ubingtu这个次虚拟机的操作界面里

[PVE内部虚拟机里创建的ubungtu容器用finalshell连不上的问题解决方法](PVE内部虚拟机里创建的ubungtu容器用finalshell连不上的问题解决方法.md)



第一步更新ubungtu成国内的源
# [pve更新软件源](pve更新软件源.md)



第一步更新ubungtu成国内的源

# 更新pve软件源方法1

PVE 虚拟机主机 更换国内源以及解决无效订阅的问题

1、PVE更换国内源

注：本文以 pve 7.3.3 为例。

替换前建议先更新下证书，否则可能由于证书不可用导致 https 无法使用，进而无法下载所有软件。

```
apt install apt-transport-https ca-certificates
```

注意：这个步骤出现错误就反复重复运行上面这条命令直到成功，有时候网络不好会失败

首先替换通用软件源， Debian 的软件源配置文件是 /etc/apt/sources.list

```
cd /etc/apt/
```

```
ls
```


发现sources.list文件

```
vi /etc/apt/sources.list
```


如果编辑错误会自动生成一个
/etc/apt/.sources.list.swp
文件

这时候要删除这个文件

```
rm /etc/apt/.sources.list.swp
```



备份后将其中内容修改为以下即可。

进去以后先进入编辑模式
a 然后手动输入一个deb

这里用阿里的软件源
https://developer.aliyun.com/mirror/ubuntu?spm=a2c6h.13651102.0.0.3e221b113SE1l6
注意复制的代码对应的系统要和我的系统和版本是一致的
例如
ubuntu 18.04(bionic) 配置如下

```
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free

deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free

deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free
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


保存操作
ctrl+c 再输入 
```
:wq
```
保存

或者用nano方式编辑的话就是
ctrl+x 再按Y，回车，就可以完成。

之后替换 pve 软件源，pve 镜像默认的 pve 软件源配置文件是 /etc/apt/sources.list.d/pve-enterprise.list ，备份后将其中内容替换为以下即可：(修改步骤同前面。)

```
cd /etc/apt/sources.list.d/
```


```
vi /etc/apt/sources.list.d/pve-enterprise.list
```


```
rm /etc/apt/sources.list.d/.pve-enterprise.list.swp
```

vi进去按a是在当前光标的下一格输入
按i是在当前光标插入
按o是在当前光标的下一格输入




```
deb https://mirrors.tuna.tsinghua.edu.cn/proxmox/debian bullseye pve-no-subscription
```


# [PVE网络不好或终端连不上linux网络不好](PVE网络不好或终端连不上linux网络不好.md)




一、更新PVE软件源

```
sudo apt update
```

```
sudo apt upgrade -y
```



```
apt install git 
```


```
apt install git qemu-utils make -y
```








回到root根目录
```
cd ~
```
下一步可以手动下载一个蒙特雷系统
或者命令直接下载
```
git clone https://github.com/thenickdude/osx-KVM.git
```

```
cd /root/osx-KVM/scripts/monterey
```


有时候前面下载那个命令没下载完全cd这里进不去，会说不存在这个文件

把下载的文件和文件夹全删了重新来一次

```
git clone https://github.com/thenickdude/osx-KVM.git
```

[PVE网络不好或终端连不上linux网络不好](PVE网络不好或终端连不上linux网络不好.md)

```
cd /root/osx-KVM/scripts/monterey
```


```
make Monterey-recovery.img
```

```
ls
```

出现四个文件
Basesystem.chunklist
Basesystem.dmg Makefile
Monterey-recovery.dmg
Monterey-recovery.img

下一步
# A2:回到主PVE的操作界面
# 将镜像从容器拖进宿主里

在pve的网页上
打开pve》shell
会出现另一个linux系统的命令输入窗口

```
pct pull 100 /root/osx-KVM/scripts/monterey/Monterey-recovery.img /var/lib/vz/template/iso/Monterey-recovery.img
```


## 下载opencore



首先来到存放iso的目录

```
cd /var/lib/vz/template/iso/
```

```
ls
```
发现蒙特雷的镜像文件
Monterey-recovery.img
已经在里面了
就等于是用opencore引导到我们的恢复镜像再从恢复镜像中将系统从互联网中拖下来安装到我们虚拟机的硬盘里面是这样一个流程

这里用wget命令来获取opencore的镜像


```
wget https://github.com/thenickdude/KVM-Opencore/releases/download/v15/openCore-v15.iso.gz
```
如果没反应说明网速没能连接到github的网站
多试几次
```
wget https://github.com/thenickdude/KVM-Opencore/releases/download/v15/openCore-v15.iso.gz
```

用gzip命令解压

```
gzip -d openCore-v15.iso.gz
```







# 新建苹果系统的虚拟机
打开pve的网页
新建一个VM虚拟机

右上角创建虚拟机
```
----------
常规
----------
节点pve
VMID 101
名称 随便写  例如 macOS1
----------
操作系统
----------
存储local
ios镜像openCore-v15.iso
类别  linux
版本 6x -2.6kermel
----------
系统
----------
显卡     VMWare兼容
机型     q35
BIOS     OVFM（UEFI）
SCSI控制器
添加EFI磁盘 打勾
EFI storage 选择local-lvm
Pre-Enroll keys 去掉勾选
SCSI控制器 VirtlO SCSI
Qemu代理   打勾
Add TPM  不打勾
预注册密钥 不打勾
----------
磁盘
----------
磁盘
总线/设备：VirtlO Block   ,  0
存储：local-lvm
磁盘大小 1024 G
缓存  Write back(不安全)


IO thread:不勾选
只读：不勾选
跳过复制：不勾选
备份：勾选
Async IO:默认(io_uring)


----------
CPU
----------
插槽1
核心8
类别Penryn

VCPUs:8
CPU权重：100
CPU限制：无限制
启用NUMA:打勾

----------
内存
----------
 16384 mb


----------
网络
----------
无网络设备  不勾选
桥接  vmbr0
模型：  Virtlo(半虚拟化)
VLAN标签： no VLAN
MAC地址： auto
防火墙：打勾
断开：不勾选
速率限制(MB/s:unlimited
Multiqueue:空着

----------
确认
----------
勾选高级

完成


```


注意前面填之前要查看一下pve这台硬件的内存有多少
free -m
15g就是15360mb

也要查看一下pve这台硬件的硬盘有多少
free -m
16g就是16384mb


接下来左边就会有这个101虚拟机

点击这个macOS系统的101虚拟机》硬件》添加CD DVD驱动器

```
创建：CD/DVD Drive
总线/设备：IDE ,  0
勾选使用CD/DVD光盘镜像文件(ISO)
存储：local
ISO映像：Monterey-recovery.img
不勾选 使用物理CD/DVD驱动器
不勾选 不使用任何介质
创健
```






# 回到PVE主机器界面
避免循环引导
```
echo "options kvm ignore_msrs=Y">>/etc/modprobe.d/kvm.conf && update-initramfs -k all -u
```

出现
update-initramfs: Generating /boot/initrd.img-5.15.102-1-pve
Running hook script 'zz-proxmox-boot'..
Re-executing '/etc/kernel/postinst.d/zz-proxmox-boot'in new private mount namespace..
No /etc/kernel/proxmox-boot-uuids found,skipping ESP sync.
就成功了





接下来用文本修改器修改它的配置文件

刚才数去避免循环引导那里
点击主的pve机器
    > shell

修改/etc/pve/qemu-server/101.conf文件

```
cd /etc/pve/qemu-server/
```


```
vi /etc/pve/qemu-server/101.conf
```




如果是intel的cpu那么下面这两行之间添加
```
agent:1

bios:ovmf
```

也就是说如果再难哦里添加下面这些

```
<msi=off -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
```


它会变成
```
args: -device isa-applesmc,osk="这里得自己百度上找" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
```

自己找的部分
百度搜索
```
-device isa-applesmc,osk=
```
-device isa-applesmc,osk=


搜到
一串苹果的OSK代码

-device isa-applesmc,osk=ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc
也就是
```
ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc
```
翻译过来就是
我们的努力被这些话保护着请不要偷苹果电脑公司


加入"这里得自己百度上找"这里以后是



```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
```

将里面有media=cdrom    的地方改成  cache=unsafe
也就是
将这里
```
ide0:local:iso/Monterey-recovery.img,media=cdrom size=3133040K
ide2:local:iso/opencore-v15.iso,media=cdrom,size=150M
```


改成
```
ide0:local:iso/Monterey-recovery.img,cache=unsafe,size=3133040K
ide2:local:iso/openCore-v15.iso,cache=unsafe,size=150M
```




变成

```
agent:1
<msi=off -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
bios:ovmf
```


也就是说
最后这个文件变成这样了

```
agent: 1
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
bios: ovmf
boot: order=virtio0;ide2;net0;ide0
cores: 8
cpu: Penryn
efidisk0: local-lvm:vm-101-disk-0,efitype=4m,size=4M
ide0: local:iso/Monterey-recovery.img,cache=unsafe,size=3144712K
ide2: local:iso/openCore-v15.iso,cache=unsafe,size=150M
machine: q35
memory: 16384
meta: creation-qemu=7.2.0,ctime=1687273660
name: mac
net0: virtio=8E:DF:81:9E:9D:77,bridge=vmbr0,firewall=1
numa: 1
ostype: other
scsihw: virtio-scsi-single
smbios1: uuid=adfd3c1c-382d-4dc1-bee1-cd13052ebfe5
sockets: 1
vga: vmware
virtio0: local-lvm:vm-101-disk-1,cache=unsafe,iothread=1,size=1T
vmgenid: 5e1474f9-1ab9-4010-b7b9-2f8b1b1ff81c

```






### 如果有错误

如果出现启动不了
并且提示
TASK ERROR: no such logical volume pve/vm-101-disk-1
翻译过来是
任务错误：没有这样的逻辑卷pve/vm-101-disk-1




如果出现下面提示并卡很久就重新装下，macOS这个虚拟机
下面提示出现再pve界面
kvm: type=2-device: Could not open 'type=2-device': No such file or directory  
TASK ERROR: start failed: QEMU exited with code 1
意思是
kvm:type=2-device:无法打开'type=2-divice'：没有这样的文件或目录
任务错误：启动失败：QEMU退出，代码为1
检查见面输入的代码 ，肯定是细节出错了。没有空格的地方要空格


如果出现PVE界面卡很久
然后提示
Start PXE over IPv6.
PXE-E16:No valid offer received.
BdsDxe:failed to load Boot0005 "UEFI PXEv6 (HAC:924ABDF33852)"from PciRoot (0x0)/Pci(Ox1E.0x0)/Pci(0x1.0x0)/Pci (0x12,0x0)/MAC (924ABDF33852.0x1)/IPu6(0000:0000
0000:0000:0000:0000:0000:0000,0x0,Static,0000:0000:0000:0000:0000:0000:0000:0000,0x40,0000:0000:0000:0000:0000:0000:0000:0000):Not Found
意思是
通过IPv6启动PXE。
PXE-E16:未收到有效报价。
BdsDxe:无法从
PciRoot(0x0)/Pci(Ox1E.0x0)/Pci(0x1.0x0)/Pci(0x12,0x0)/MAC (924ABDF33852.0x1)/IPu6(0000:0000
加载
Boot0005 "UEFI PXEv6 (HAC:924ABDF33852)


0000:0000:0000:00000:0000,0x0，静态，0000:0000:0.000:0000,0000:00000,0x400000:0000:000:0000:0000）：未找到


然后进去提示是
UEFI Interactive Shell v2.2
EDK II
UEFI v2.70 (EFI Development Kit II OVMF,0x00010000)
Mapping table
FS1:Alias (s):HD1b65535a1::BLKS:
PciRoot (0x0)/Pci (0x1F,0x2)/Sata (0x1,0xFFFF,0x0)/HD(1.GPT DF00D630-AE41-4232-B6B7-7B6EFEAD06A4.0x28.0x4AFBO)
FS0:Alias (s):HD1a65535a1:BLK2:
PciRoot (0x0)/Pci (0x1F,0x2)/Sata (0x0,0xFFFF,0x0)/HD(1,GPT,A3C47B91-A91D-4D5A-99ED-352B2AFE2EB8,0x28,0x64000)
BLKO:Alias(s):
PciRoot (0x0)/Pci(0x1E,0x0)/Pci (0x1,0x0)/Pci(0xA,0x0)
BLK4:Alias(s):
PciRoot (0x0)/Pci(0x1F,0x2)/Sata (0x1,0xFFFF,0x0)
BLK1:Alias(s)
PciRoot (0x0)/Pci(0x1F,0x2)/Sata (0x0,0xFFFF,0x0)
BLK3:Alias(s):
PciRoot (0x0)/Pci (0x1F,0x2)/Sata (0x0,0xFFFF,0x0)/HD (2,GPT,9CBDSA47-E8E6-44AD-83B2-14AB83DB3B2D,0x64028,0x55B7C0)
Press ESC in 1 seconds to skip startup.nsh or any other key to continue
Shell>
意思是
UEFI交互式Shell v2.2
EDK II公司
UEFI v2.70（EFI开发套件II OVMF，0x00010000）
映射表
FS1:别名：HD1b65535a1:：BLKS：
PciRoot（0x0）/Pci（0x1F，0x2）/Sata（0x1,0xFFFF，0x0）/HD（1.GPT DF00D630-AE41-4232-B6B7-7B6EFEAD06A4.0x28.0x4AFBO）
FS0:别名：HD1a65535a1:BLK2:
PciRoot（0x0）/Pci（0x1F，0x2）/Sata（0x0,0xFFFF，0x0）/HD（1，GPT，A3C47B91-A91D-4D5A-99ED-352B2AFE2EB8,0x28,0x64000）
BLKO：别名：
PciRoot（0x0）/Pci（0x1E，0x0）/Pci（0x1,0x0）/Pcci（0xA，0x0
BLK4：别名：
PciRoot（0x0）/Pci（0x1F，0x2）/Sata（0x1,0xFFFF，0x0）
BLK1:别名
PciRoot（0x0）/Pci（0x1F，0x2）/Sata（0x0,0xFFFF，0x0）
BLK3:别名：
PciRoot（0x0）/Pci（0x1F，0x2）/Sata（0x0,0xFFFF，0x0）/HD（2，GPT，9CBDSA47-E8E6-44AD-83B2-14AB83DB3B2D，0x64028,0x55B7C）
1秒钟后按ESC跳过启动。sh或任何其他键继续
外壳>


参考
[opencore如何配置linux启动](opencore如何配置linux启动.md)



关机时
如果出现提示是
TASK ERROR: VM quit/powerdown failed - got timeout




如果出现提示是
trying to acquire lock...  
TASK ERROR: can't lock file '/var/lock/qemu-server/lock-101.conf' - got timeout
意思是
正在尝试获取锁。。。
任务错误：无法锁定文件“/var/lock/qemu server/lock-101.conf”-超时

```
update-grub
```



### 如果没错误

就会顺利进入到opencore系统
这时候需要联网的

并且看到引导的硬盘
这时候回车
就看见苹果的标志了
苹果标志过了以后

点击下面    磁盘中心 Disk Utility
然后点击   继续 continue


就进入到可以把硬盘格式化一下的界面了
这里点击第一个  Apple Inc.VirtlO Block Media

点击右上角的 erase 擦除


name这里创建一个名字随便写 例如 Untitled
Format:  APFS
Scheme:GUID Partition Map

然后Erase
Down

接下来叉掉X这个工具

回到四行这个界面


Reinstall macOS Monterey

continue

agree agree 
选择 我们的硬盘
然后continue

它就会自动重启几次

第一次重启记得选择macOS installer 

第二次重启也是选择macOS installer 

第三次 重启 选择刚才设置的名字例如  Untitled

最后一次重启 还是选择刚才设置的名字例如  Untitled


就进入初始化流程了

选中国 下一步 not mow 继续

Migration Assistant是恢复界面 
选择左下角 不恢复  not mow

暂时不登录苹果id也就是 not mow

agree agree 

设置一个账号密码 

不激活location定位 不勾选


















[PVE网络不好或终端连不上linux网络不好02](PVE网络不好或终端连不上linux网络不好02.md)
