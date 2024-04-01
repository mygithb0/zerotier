# zerotier

Network ID
e3918db4837fb16b

openWRT网页
```
http://172.25.4.194/
root
dxdll12345
```
Alist网盘的webDAV
http://172.25.4.194:8888
```
dxdll10001
dxdll12345
```

http://172.25.245.132:5244
admin
123456

iStoreOS的openWRT用来同步obsidian的
```
iStoreOS的openWRT设置网页
http://172.25.245.132/

root
a

Alist网盘的webDAV

http://172.25.245.132:5244
admin
123456

```



ubungtu用来同步obsidian的
```
\\172.25.46.223
Alist账号 admin
Alist密码 123456
同步webdav网址   http://172.25.46.223:5244/dav
主页网址         http://172.25.46.223:5244/@manage/users
开机账号  a
开机密码  a
```
[装有linux系统硬盘每次更换电脑都要重新绑定网卡名称ubungtu或者pve也适用否则不能上网也不能ping通网关](装有linux系统硬盘每次更换电脑都要重新绑定网卡名称ubungtu或者pve也适用否则不能上网也不能ping通网关.md)

小笔记本 用户名字 1
```
\\172.25.55.228
```
小笔记本音乐硬盘 用户名字 1
```
\\172.25.167.20
```
超微win10画图主盘  用户名字 1
共享文件夹密码就是开机密码，开机密码是1
```
\\172.25.146.85
```

PVE192.168.0.20
win10访问linux可以在运行命令下输入IP地址
```
\\172.25.112.93\share
```



win11盘  用户名字b
```
\\172.25.216.32
```
iphone esim
```
\\172.25.88.86
```
苹果手机访问windows电脑共享文件夹方法：
苹果里面“文件”>连接服务器

# 设置zerotier下的共享文件夹
选择一个想要共享的文件夹》右键》属性》

属性》共享》下拉箭头选择everyone》共享》完成

高级共享》权限》完全控制 更改 读取

高级共享》权限》添加》高级》立即查找》everyone ，everyone就添加进去了

属性》安全》编辑》所有权限全打勾打开

属性》安全》编辑》everyone>添加》高级》立即查找》下面选择everyone》确定确定

# 设置zerotier下的共享的电脑环境

控制面板》网络和internet》网络和共享中心》高级共享设置》启用共享以便可以访问......   无密码保护共享

搜索框 本地组策略编辑器》windows设置》安全设置》本地策略》安全选项》右边找到:账户：使用空白密码的本地账户只允许进行控制台登录的选项，双击，在弹出的窗口中，上方点选上以禁用然后依次点击确定


# 开机自启动zerotier

把zerotier的快捷方式从这里复制
```
C:\ProgramData\Microsoft\Windows\「开始」菜单\程序
```

或者是英文的地址
```
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\
```


复制进这里：
```
C:\ProgramData\Microsoft\Windows\「开始」菜单\程序\启动
```
或者是英文的地址这个里：
```
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup
```

# obsidian文件夹在C盘
```
C:\ProgramData\10logseq-win11-20231116
```

# obsidian文件夹在z盘
```
Z:\
```
# 电脑之间传文件的同步文件夹在V盘
```
V:\
```

# [PVE装新机](PVE装新机.md)

