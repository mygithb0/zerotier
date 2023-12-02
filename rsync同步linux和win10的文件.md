在linux主机里设置一个windows共享文件夹的挂载文件夹

```
mount -t cifs -o username=电脑win10的账号,password=电脑win10的密码  //电脑win10的IP地址密/共享文件夹名称 /winshare/
```


例如



电脑win10的账号是1。电脑win10的密码是1。输入windows主机的地址也就是172.25.146.85这个数字。共享文件夹的文件名是10logseq20230504这个文件名

那么输入的内容就是

```
mount -t cifs -o username=1,password=1 //172.25.146.85/10logseq20230504 /winshare/
```


查看挂载是否成功了
```
df -HT
```





windos同步去linux的方法
```
rsync -av /winshare/ /linux里的路径/linux里的共享文件夹/
```
linux同步回来windos的方法
```
rsync -av /linux里的路径/linux里的共享文件夹/ /winshare/
```



例如

windos同步去linux的方法
```
rsync -av /winshare/ /root/share/logseq/10logseq20230504/
```
linux同步回来windos的方法
```
rsync -av /root/share/logseq/10logseq20230504/ /winshare/
```

也就是说是
rsync -a /起点路径/要复制的文件夹/ /终点路径/同步到的文件夹
或者把/路径/文件夹/改为winshare






