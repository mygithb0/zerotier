

# [先解决apt无法更新和make命令无法使用的问题](先解决apt无法更新和make命令无法使用的问题.md)




https://blog.csdn.net/hlz_07/article/details/122229311

pve安装时设置dns8.8.8.8,或者winscp软件修改/etc/resolv.conf文件即可
1、安装curl命令支持
```
apt-get install curl
```


2、安装gnupg非对称信息加密系统，通讯所需必备软件
```
apt-get install gnupg
```


3、安装ZeroTier
```
curl -s https://install.zerotier.com/ | bash
```


安装成功后提示如下：
Success! You are ZeroTier address [ 19f34350c3 ].
方括号内地址为Zerotier系统指定，每台电脑都不同，我的理解类似于MAC地址。

4、设定开机自启动（分别执行如下命令）
```
systemctl start zerotier-one.service
```


```
systemctl enable zerotier-one.service
```


如果失败，再执行一次命令。

5、加入自己的私有网络如果zerotirt给的号是93afXXXXX
那么命令就是
```
zerotier-cli join 93afXXXXX
```

例如
```
zerotier-cli join e3918db4837fb16b
```


光猫要桥接才能发现设备
