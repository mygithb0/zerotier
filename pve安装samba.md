
```
sudo apt-get install samba
```

```
samba version
```



2.创建共享文件夹
```
sudo mkdir /path/to/shared_folder
```


例如
在root目录下新建一个share文件夹例如
```
sudo mkdir /root/share
```

在root目录下share目录下新建一个logseq文件夹例如
```
sudo mkdir /root/share/logseq
```

在root目录下share目录下新建一个share2文件夹例如
```
sudo mkdir /root/share/share2
```



3.创建Samba用户(这一步不用了)
将user_1替换为要创建的Samba用户名，然后根据提示设置密码
1
sudo smbpasswd -a user_1

例如
sudo smb12345 -a a1

如果出现
[smb command not found](smb%20command%20not%20found.md)









安装Samba服务器
```
sudo apt install samba
```


配置smb.conf


sudo vim /etc/samba/smb.conf

或者用finashell手动下载打开/etc/samba/smb.conf再上传进去

[复制进smb.conf的代码](复制进smb.conf的代码)




smb.conf设置教程参见
[samba 配置教程](samba%20配置教程)
或者
https://blog.csdn.net/2201_75288693/article/details/130941304




sambal的配置文件位于/etc/samba/smb.conf,这个文件应该告诉系统应该共享哪些目录、它们的访问权限和更多选项。默认的smb.conf
已经带有大量注释代码，您可以使用这些代码作为示例来编写自己的配置。

进入/etc/samba/smb.conf

重新启动sambal服务

```
sudo service smbd restart
```



通过Windows访问samba共亨
在Windows中，只需在"运行"里面输入linux服务器的ip地址和分享文件夹名字
例如
```
\\172.25.112.93\share
```











