检查下网站是否能联网
用ping尝试百度网站
```
ping www.baidu.com
```

发现ping不通
所以要修改dns的配置
修改dns的配置的文件在/etc/resolv.conf 
 所以要
```
cd /etc
```
cd /etc
找到
/etc/resolv.conf 文件打开编辑


检查下网站是否能联网
用ping尝试百度网站

```
ping www.baidu.com
```
这次就成功了

执行apt更新
```
apt update
```

如果还是更新不了就
加入清华大学软件源


```
cd /etc/apt/sources.list.d/
```
找到文件/etc/apt/sources.list.d


打开sources.list文件

里面加入清华这个网页立给的这个代码
https://mirrors.tuna.tsinghua.edu.cn/help/debian/


```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free

deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free

deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free

# deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free

deb https://security.debian.org/debian-security bullseye-security main contrib non-free
# deb-src https://security.debian.org/debian-security bullseye-security main contrib non-free
```




安装net-tools工具
```
apt install net-tools
```


提示错误的话
根据提示
复制提示里面的错误的信息里面的fix XXXX这一段修复命令

出现yes的时候打y
```
y
```

再次执行apt更新
```
apt update
```
这还没成功

```
cd /etc/apt/
```

```
lsb_release -a
```


```
ls
```

删除.sources.list.swp 文件
```
rm .sources.list.swp 
```

vi sources.list
ls sources.list.d/

在tmp文件夹下新建/tmp/source文件夹
```
mkdir /tmp/source
```
mkdir /tmp/source


把pve的源文件转移到一个别的路径下不在调用pve的源
```
mv sources.list.d/* /tmp/source/
```

再次执行apt更新
```
apt update
```

这次终于成功了
因为刚才没成功，这次再次装一下net-tools工具
```
apt install net-tools
```

还是没成功
执行一下apt修复
```
apt --fix-broken install
```

因为还是没成功，这次再次装一下net-tools工具
```
apt install net-tools
```

安装make命令
```
apt install make
```
 
  ```
  makemake
  ```

设置一下make
```
make-ssl-cert  make_strings 
```
执行一下make看安装成功了没
```
make
```



其他命令
[linux查看操作的输入历史](linux查看操作的输入历史.md)
```
history
```


