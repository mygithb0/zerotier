Samba服务器的配置与管理

    1、Samba服务器配置的工作流程
        1.1 Samba工作流程
    2、解读主要配置文件smb.conf
        2.1 Global Settings
        2.2 客户端访问控制
    3、最常用的几个字段
    4、Samba服务密码文件
    5、Share服务器实例解析
    6、samba服务器客户端的配置
        6.1 Linux客户端访问Samba服务器
        6.2 利用windows客户端访问Samba共享目录
————————————————
版权声明：本文为CSDN博主「晚妍」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/2201_75288693/article/details/130941304


在Linux中，大家听的最多的可能就是Samba服务，什么是Samba呢，Samba是连接Linux与Windows的桥梁，真是由于Samba的出现，我们才可以在Linux和Windows间互相通信。
1、Samba服务器配置的工作流程

在Samba服务安装完毕之后，并不是直接可以使用Windows或Linux的客户端访问Samba服务器，我们还必须对服务器进行设置：告诉Samba服务器将那些目录共享出来给客户端进行访问。

基本的Samba服务器搭建流程主要分为四个步骤。

（1）编辑主配置文件smb.conf，指定需要共享的目录，并未共享目录设置共享权限。

（2）在smb.conf文件中指定日志文件名称和存放路径。

（3）设置共享目录的本地系统权限

（4）重新加载配置文件或重新启动SMB服务，使配置生效。
1.1 Samba工作流程

1、客户端请求访问Samba服务器上的共项目录

2、Samba服务器接收到请求后，会查询主配置文件smb.conf，看是否共享了share目录，如果共享了则查询客户端是否有权限访问。

3、Samba服务器会把本次访问信息记录写在日志中，日志文件的名称和路径都需要我们设置。

4、如果客户端满足访问权限的设置，则允许客户端进行访问。

![](45f56e40c19836949b4f4c91e60118de.png)


2、解读主要配置文件smb.conf

Samba的配置文件一般就放在/etc/samba目录中。主配置文件名为smb.conf，如果把Samba服务器比喻成一个图书馆，那么smb.conf就相当于这个图书馆的图书总目录，记录着大量的共享信息和规则，是samba服务器的核心。
2.1 Global Settings

Global settings 设置为全局变量区域。全局变量区域就是我们只要在Global是进行设置，那么该设置项目就是针对所有共享资源生效的，这与我们以后需要学习的很多服务器配置很相像。

```
[global]
        workgroup = SAMBA			//设置工作组或域名
        security = user					//设置安全模式

        passdb backend = tdbsam

        printing = cups
        printcap name = cups
        load printers = yes
        cups options = raw

```

[Global]常用字段及设置方法如下

（1）设置工作组或域名称

工作组是网络中地位平等的一组计算机，可以通过设置workgroup字段来对Samba服务器所在工作组或域名进行设置。

（2）设置Samba服务器安全模式

Samba服务器一共share,user,server,domain和ads五种安全模式。

1、share安全级别模式。客户端登陆Samba服务器、不需要输入用户名和密码就可以浏览Samba服务器的资源，适用于公共的资源共享，安全性差，需要配合其他权限进行设置。保证Samba服务器的安全性。

2、user安全级别模式。客户端登陆Samba服务器、需要输入指定的用户名和密码才能进行浏览Samba服务器的资源，服务器默认为此级别模式。

3、server安全级别模式。客户端需要将用户名和密码提交到指定的一台Samba服务器上进行验证，如果验证出现错误，客户端会使用user级别访问。

4、domain安全级别模式。如果Samba服务器加入Windows域环境中，验证工作将由Windows域负责，domain级别的Samba服务器这是成为域的成员客户端，并不具备服务器的特性。
2.2 客户端访问控制

对于Samba服务器的安全性，可以使用vliad users字段去实现用户控制访问，但是如果企业庞大且存在大量的用户的话，这种方法操作起来就比较的麻烦。所以我们可以使用hosts allow和hosts deny两个字段可以实现该功能。

hosts allow和hosts deny字段的使用

```
hosts allow 字段定义允许访问的客户端
hosts deny 字段定义禁止访问的客户端
```

Samba服务器中有个目录为/share。需要发布该目录成为共享目录，定义共享目录名为public。

## 3、最常用的几个字段

（1）**设置共享名**。  
共享资源发布后，必须为每个共享目录设置不同的共享名，给网络用户访问时使用，并且共享名可以以原目录名不同。
```
格式：
[共享名]
```

（2）**共享资源描述**。  
网络中存在各种共享资源，为了方便用户识别，可以为其添加备注信息，以方便用户查看时知道共享资源的内容是什么。
```
comment = 备注信息
```

（3）**共享资源路径**。  
共享资源的原始完整路径，可以使用path字段进行发布，务必正确指定。
```
path = 资源的绝对路径
```

（4）**设置匿名访问**。  
这只是否允许对共享资源进行匿名访问。

```
public = yes    //允许匿名访问
public = no   //不允许匿名访问
```

（5）**设置访问用户**。

如果共享资源存在重要数据的话，需要对访问用户审核，我们可以使用valid users字段进行设置。

```
valid users = 用户名
valid users = @组名
valid users = @组名，用户名
```

例：samba服务器共享文件为/share/tech目录，只允许组tech，和用户manager访问
```
comment=users   //可不加
path=/share/tech
valid users = @tech，manager
```

(6)**设置目录只读**。

共享目录如果限制用户的读写操作，我们可以通过read only 实现。

```
read only = yes //只读
read only = no  //读写
```

例：samba服务器公共目录/public存放大量共享数据，为保证目录安全，我们只允许读取，禁止写入。
```
comment = public
path = /public
public = yes
read only = yes
```


(7)**设置目录可写**

如果共享目录允许用户写操作，可以使用writable或write list 两个字段进行设置。
```
writable = yes   //读写
writable = no    //只读
```

**write list**
```
write list = 用户名
write list =@组名
```

4、Samba服务密码文件

samba服务器发布共享资源后，客户端访问samba服务器，需要提交用户名和密码进行身份验证，验证合格才可以登录。Samba服务器为了实现客户身份验证功能，将用户名和密码存放在/etc/samba/smbpasswd中，在客户端访问时，将用户提交的资料与smbpasswd存放的信息进行比对，如果相同，客户端与samba服务器的连接才能建立成功。

那如何建立Samba账号呢。首先我们要创建一个系统账号，例如toto。

创建完成之后我们使用下方命令在samba服务中创建账号
```
useradd toto     //创建系统账号
passwd toto		//设置密码
smbpasswd -a  toto  //创建samba服务账号
```

5、Share服务器实例解析

下面我们介绍该如何配置samba的服务端，并顺带做一个项目实例

某公司需要添加samba服务器作为文件服务器，共享目录为/share，共享名为public，这个共享目录允许所有员工访问。

解析：这个共享目录允许所有员工访问，因为我们不知道这个所有他到底是多少，所以为了方便管理，我们直接使用匿名访问，这样会简单很多。

1建立share目录，并在其下建立测试文件

```
mkdir /share
toch /share/toto
```

修改samba主配置文件smb.conf
```
[global]
        workgroup = SAMBA
        security = user
        map to guest = bad user
        guest ok = yes
[public]
        path = /share
        browseable = yes
        public = yes

```

修改文件/share的所有者和权限
```
[root@localhost ~]# mkdir /share
[root@localhost ~]# chmod 777 /share/
[root@localhost ~]# chown nobody.nobody /share

```

重新加载配置文件
```
[root@localhost ~]# systemctl restart smb nmb
```
关闭防火墙和禁用selinux
```
[root@localhost ~]# systemctl stop firewalld
[root@localhost ~]# setenforce 0
```
通过以上设置，用户就可以在不输入账户和密码的情况下直接登录samba服务器并访问目录public。

6、samba服务器客户端的配置

我们可以使用两种不同的方法，在windows客户端和linux客户端之间进行登录samba服务器
6.1 Linux客户端访问Samba服务器

使用smbclient命令

我们在使用smbclient时，先要确保安装了samba-client这个软件包。
```
yum install -y samba-client
```

smbclient可以列出目标主机共享目录列表。格式如下：

smbclient -L 目标IP地址 -U 登录用户名

当我们查看IP地址为172.168.1.1的IP地址主机时，不输入用户的话，我们会看到以下内容，这就是表示匿名用户能看到的共享目录列表。

```
[root@localhost ~]# smbclient -L 172.168.1.1
Enter SAMBA\root's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        public          Disk      
        IPC$            IPC       IPC Service (Samba 4.10.16)
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        SAMBA                LOCALHOST

```

我们还可以使用smbclient命令行共享访问模式浏览共享的资料。

smbclient命令行共享访问模式命令格式：

**`smbclient //目标IP地址或主机名/共享目录 -U 用户名%密码`**

例：当samba服务器的共享目录为public并且用户toto可以登录时

```
smbclient //172.168.1.1/public -U toto%123456
```

例：当samba服务器的共享目录为public并且匿名用户可以登录时
```
[root@localhost ~]# smbclient //172.168.1.1/public 
Enter SAMBA\root's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Tue May 30 08:56:31 2023
  ..                                  D        0  Tue May 30 08:50:38 2023
  toto                                D        0  Tue May 30 08:56:31 2023

                17811456 blocks of size 1024. 15658328 blocks available

```

### 6.2 利用windows客户端访问Samba共享目录

windows客户端访问samba共享目录的方法有很多，这里展示其中两种：

1.首先我们按住win+R键，然后输入以下内容

![](4aee387788b78245df158b9d8fa7bb8e.png)


点击确定，我们就可以直接登录samba服务器了

![](3203b2291c45d1d73d5a0a4d899d64c9.png)

方法二、我们点击此电脑，或者任意文件夹后，点击此电脑。

![](8be204532797b51cb35aec251433385b.png)

找到映射网络驱动器。

![](8c4c452a11f0598a5865fcdb4b9318b0.png)

点击，并输入samba服务器的ip地址和共享目录
![](d14ddb36686a61e0d9c93b4362c5c96e.png)

最后我们就可以登录samba服务器了。