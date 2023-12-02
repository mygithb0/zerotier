删除已安装的mysql

[http://www.360doc.com/content/22/0114/12/78411425_1013214754.shtml](https://link.zhihu.com/?target=http%3A//www.360doc.com/content/22/0114/12/78411425_1013214754.shtml)

[https://www.jianshu.com/p/7b6b8a5689f0](https://link.zhihu.com/?target=https%3A//www.jianshu.com/p/7b6b8a5689f0)

卸载

sudo apt-get autoremove --purge mysql-server

sudo apt-get autoremove mysql-server

sudo apt-get remove mysql-common

sudo apt-get -f install

sudo apt autoremove

sudo apt-get remove --purge mysql-\*

  

---------------------------------------------------------repo apt安装方法-------------------------------------------------------------------

[https://blog.csdn.net/qq_30818545/article/details/122868975](https://link.zhihu.com/?target=https%3A//blog.csdn.net/qq_30818545/article/details/122868975)

1. 首先更新本地存储库索引，执行

sudo apt update && sudo apt upgrade && sudo apt install lsb-release && sudo apt install gnupg

  

2. MySQL 在默认的 Debian 存储库中不可用。您需要在 Debian 11 上安装 MySQL APT 存储库：

[https://dev.mysql.com/downloads/repo/apt/](https://link.zhihu.com/?target=https%3A//dev.mysql.com/downloads/repo/apt/)

wget [https://repo.mysql.com/mysql-apt-config_0.8.24-1_all.deb](https://link.zhihu.com/?target=https%3A//repo.mysql.com/mysql-apt-config_0.8.24-1_all.deb) --no-check-certificate

sudo dpkg -i mysql-apt-config_0.8.24-1_all.deb

  

在 MySQL 存储库安装过程中，如果出现提示，请选择 Debian buster 的存储库，然后按 TAB 键选择 Ok。按 ENTER 继续。

接下来，通过运行以下命令更新包列表并安装 MySQL 服务器包：

选择debian buster

选择MySQL Server Cluster (Currently selected:mysql-8.0)

选择mysql-8.0

选择OK

sudo apt update


> 如果出现以下错误  
>   
> 错误:5 [http://repo.mysql.com/apt/debian](https://link.zhihu.com/?target=http%3A//repo.mysql.com/apt/debian) buster InRelease  
>   
> 由于没有公钥，无法验证下列签名： NO_PUBKEY 467B942D3A79BD29  
>   
> 正在读取软件包列表... 完成  
>   
> W: GPG 错误：[http://repo.mysql.com/apt/debian](https://link.zhihu.com/?target=http%3A//repo.mysql.com/apt/debian) buster InRelease: 由于没有公钥，无法验证下列签名： NO_PUBKEY 467B942D3A79BD29  
>   
> E: 仓库 “[http://repo.mysql.com/apt/debian](https://link.zhihu.com/?target=http%3A//repo.mysql.com/apt/debian) buster InRelease” 没有数字签名。  
>   
> N: 无法安全地用该源进行更新，所以默认禁用该源。  
>   
> N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节  
>   
> 手动执行：报错信息中的NO_PUBKEY的值 467B942D3A79BD29  
>   
> **sudo apt-key adv --keyserver [http://keyserver.ubuntu.com](https://link.zhihu.com/?target=http%3A//keyserver.ubuntu.com) --recv-keys 467B942D3A79BD29**  
> sudo apt update  

安装

sudo apt install mysql-server

在安装过程中，会出现一个新的弹出窗口，提示您输入数据库 root 密码。

Use Strong Password Encryption (RECOHMENDED)


安装完成后，MySQL服务将自动启动，您可以通过键入以下内容进行验证：

sudo apt policy mysql-server

sudo systemctl status mysql

> sudo systemctl enable mysql # 开机开启mysql  
> sudo systemctl disable mysql # 禁用mysql  
> sudo systemctl restart mysql # 重启mysql  
> sudo systemctl stop mysql # 关闭mysql  
> sudo systemctl status mysql # 查看mysql运行状态

9.防火墙

sudo ufw allow 3306/tcp

sudo ufw status

Status: active

  

To Action From

-- ------ ----

22/tcp ALLOW Anywhere

Nginx Full ALLOW Anywhere

3306/tcp ALLOW Anywhere

22/tcp (v6) ALLOW Anywhere (v6)

Nginx Full (v6) ALLOW Anywhere (v6)

3306/tcp (v6) ALLOW Anywhere (v6)

  

如果仍然出现远程访问 Ubuntu上的Myql时，报10061错误

# sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf

修改如下

bind-address = 127.0.0.1

mysqlx-bind-address = 127.0.0.1

为

bind-address = 0.0.0.0

mysqlx-bind-address = 0.0.0.0

  

重启 sudo systemctl restart mysql.service

