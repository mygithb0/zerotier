1finalshell连不上的信号是 反复要求输入密码 也就是说密码不对，但是输入的密码是正确的

 
   67  ip a
   68  netstat -lntp
   69  ps -ef |greo ssh
   70  ps -ef |grep ssh
   71  lsb_release -a


更新软件源成阿里的软件源

   72  vi /etc/apt/sources.list
把下面这段替换粘贴进去

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


73  apt update
没有任何错误的成功以后

74  apt install sshd
75  apt install ssh


 
下一步：
[PVE内部虚拟机里创建的ubungtu容器用finalshell连不上的问题解决方法](PVE内部虚拟机里创建的ubungtu容器用finalshell连不上的问题解决方法.md)


[linux更新清华大学的软件源不行怎么办](linux更新清华大学的软件源不行怎么办.md)