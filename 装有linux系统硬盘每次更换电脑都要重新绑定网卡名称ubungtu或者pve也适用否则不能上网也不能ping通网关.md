
# 查询网卡名字
网卡名称是用ip a命令
出来以后序号2 后面的名字

例如假如输入
root@a:~# ip a 
以后
假如出现
```
root@a:~# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 30:85:a9:73:e8:7f brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.103/24 metric 100 brd 192.168.0.255 scope global dynamic enp2s0
       valid_lft 7068sec preferred_lft 7068sec
    inet6 fe80::3285:a9ff:fe73:e87f/64 scope link 
       valid_lft forever preferred_lft forever
3: wlp3s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 9c:b7:0d:f5:b6:6a brd ff:ff:ff:ff:ff:ff
4: ztk4jpebpi: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 2800 qdisc pfifo_fast state UNKNOWN group default qlen 1000
    link/ether 6a:f0:3d:00:d3:df brd ff:ff:ff:ff:ff:ff
    inet 172.25.46.223/16 brd 172.25.255.255 scope global ztk4jpebpi
       valid_lft forever preferred_lft forever
    inet6 fe80::68f0:3dff:fe00:d3df/64 scope link 
       valid_lft forever preferred_lft forever

```

## 那么序号2 后面的 enp2s0 就是这台电脑网卡的名字

# 假如这个系统又是ubungtu系统

那么就修改
/etc/natplan这个文件夹里的
就修改
/etc/natplan/50-cloud-init.yaml这个文件里的内容

用nano命令进去
```
nano /etc/natplan/50-cloud-init.yaml
```

将里面的内容改成

```
network:
	ethernets:
		enp2s0:
			dhcp4:true
	version:2
	wifis:{}
```
也就是将enp0s31f6 改成  enp2s0


# 假如这个系统又是pve系统

那么就修改
/etc/network这个文件夹里的

/etc/network/interfaces这个文件

```
bridge-ports wwan0
改成
bridge-ports enp2s0
```

也就是文件里的内容从
```
auto lo
iface lo inet loopback

iface wwan0 inet manual

auto vmbr0
iface mbr0 inet static
	adress 192.168.0.211/24
	gateway 192.168.0.1
	bridge-ports wwan0
	bridge-stp off
	bridge-fd 0

iface enp0s31f6 inet manual

iface wlp4s0 inet manual
```

改成

```
auto lo
iface lo inet loopback

iface wwan0 inet manual

auto vmbr0
iface mbr0 inet static
	adress 192.168.0.211/24
	gateway 192.168.0.1
	bridge-ports enp2s0
	bridge-stp off
	bridge-fd 0

iface enp0s31f6 inet manual

iface wlp4s0 inet manual
```

编辑方法都是用nano进去

保存退出的方法都是
ctril+x 然后 y 然后 回车

